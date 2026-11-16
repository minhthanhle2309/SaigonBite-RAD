# UC13 — Design Classes, CRC Cards, and CRUD Verification

**Author:** Võ Tấn Tài — 524H0126
**Status:** Proposed design aligned with [UC13 specification](UC13.md). Decisions labelled **To Confirm** are not approved business rules.

## Design classes

| Layer | Class | Attributes (`-` private) | Operations (`+` public) | Responsibility |
|---|---|---|---|---|
| Boundary/View | `HubManagementView` | `-selectedHubId: HubId?`, `-formValues: HubInput?` | `+showHubList(items)`, `+showHub(hub)`, `+collectHubInput()`, `+showError(message)`, `+showRemovalOutcome(outcome)` | Presents permitted records and input/results; does not decide access or persistence. |
| Controller | `HubManagementController` | `-accessPolicy: HubAccessPolicy`, `-repository: HubRepository`, `-removalPolicy: HubRemovalPolicy` | `+listHubs(actor, filter)`, `+getHub(actor, hubId)`, `+createHub(actor, input)`, `+updateHub(actor, hubId, changes, expectedVersion)`, `+removeHub(actor, hubId)` | Coordinates permission, validation, lookup, write and result mapping. |
| Domain | `Hub` | `-id: HubId`, `-details: HubDetails`, `-capacitySetting: CapacitySetting`, `-version: Version` | `+create(id, details, capacity)`, `+revise(changes)`, `+validate()`, `+snapshot()` | Holds hub data and locally valid state. Capacity unit/bounds and version scheme are **To Confirm**. |
| Domain policy | `HubAccessPolicy` | `-permissionRules: PermissionRules` | `+can(actor, operation, hubId?)` | Evaluates confirmed operation-level rights. Actor/permission matrix is **To Confirm**. |
| Domain policy | `HubRemovalPolicy` | `-rules: RemovalRules` | `+assess(hub)`, `+apply(hub)` | Encapsulates confirmed dependency and delete/archive policy; implementation is pending client decision. |
| Data Access | `HubRepository` | `-dataSource: DataSource` | `+list(filter)`, `+findById(hubId)`, `+insert(hub)`, `+saveIfVersion(hub, expectedVersion)`, `+removeAccordingToPolicy(hub, outcome)` | Retrieves and persists records atomically where possible; reports duplicate, conflict and persistence errors. |

`HubInput`, `HubDetails`, `CapacitySetting`, `Version`, `RemovalRules` and result types are conceptual value types. Their fields are deliberately unspecified pending the Case Study and client decision. `expectedVersion` is a **proposed** concurrency mechanism, not a confirmed interface requirement.

### Collaboration and error mapping

1. `HubManagementView` sends a system event to `HubManagementController`.
2. The controller asks `HubAccessPolicy` for operation-level authorization before exposing protected data or writing.
3. For Create/Update, the controller constructs or revises `Hub`, invokes `validate()`, then calls `HubRepository`.
4. For Delete, the controller asks `HubRemovalPolicy` to assess dependencies before the repository applies the confirmed outcome. No hard-delete assumption is made.
5. The controller maps invalid input, not found, duplicate, stale version, blocked removal and write failure to an explicit result. The view shows that result. A lost write response requires a fresh Read before retry.

## CRC cards

| Class | Responsibilities | Collaborators |
|---|---|---|
| `HubManagementView` | Capture operation/input; display list, record, result or error. | `HubManagementController` |
| `HubManagementController` | Sequence UC13; authorize; validate; coordinate CRUD; translate failures. | `HubManagementView`, `HubAccessPolicy`, `HubRemovalPolicy`, `Hub`, `HubRepository` |
| `Hub` | Represent hub details and capacity setting; validate internal consistency; expose a snapshot. | `HubManagementController` |
| `HubAccessPolicy` | Check operation rights without embedding role guesses in the view. | `HubManagementController` |
| `HubRemovalPolicy` | Decide whether and how a hub may be removed under confirmed rules. | `HubManagementController`, `HubRepository` |
| `HubRepository` | Find, list and persist hub records; detect conflicts and persistence failure. | `HubManagementController`, `Hub` |

## CRUD verification

| Operation | Preconditions | Expected result | Error cases and no-change guarantee |
|---|---|---|---|
| Create | Actor has Create permission; submitted fields satisfy confirmed validation/uniqueness rules. | New hub with capacity setting and identifier is returned. | Unauthorized, invalid or duplicate input, write failure: no new hub. If response is lost, Read before retry. |
| Read | Actor has Read permission; requested hub exists and is visible to actor. | Current hub details and capacity setting are returned without mutation. | Unauthorized or absent hub: no protected data disclosed. |
| Update | Actor has Update permission; hub exists; changes are valid; record is current. | Updated hub is persisted and returned. | Unauthorized, absent, invalid, concurrent change or write failure: prior data preserved. |
| Delete / archive | Actor has Delete permission; hub exists; confirmed retention/dependency policy permits the action. | Confirmed removal outcome is returned. | Unauthorized, absent, blocked dependency or write failure: hub preserved. **Deletion mode is To Confirm.** |

The workbook's CRUD Check has a candidate Hub row and reports a **Gap** for Delete because the removal policy is open. This table verifies the **candidate UC13 design only**; it does not establish team-wide CRUD coverage. The proposal assigns brand/menu management to UC14, while the current workbook flags its ownership conflict with UC13. UC14 is not silently absorbed into UC13.

## Consistency checks

- UC13 specification, Activity, SSD and class operations use the same four verbs: Create, Read, Update, Delete (represented by `removeHub` pending policy).
- All write paths validate authorization and input; Delete also evaluates confirmed dependencies.
- No class computes overload, reroutes customer orders or changes `Order`; those behaviours require separate scope confirmation.
