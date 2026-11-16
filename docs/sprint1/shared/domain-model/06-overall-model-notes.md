# Overall Domain and Order State Model — Review Notes

**Author:** Võ Tấn Tài — 524H0126

**Status:** Proposed integration model for UC03, UC04, UC07, UC10, UC13 and UC16. This does not replace the UC07/UC10 diagrams by Lê Đỗ Minh Thành. The original Case Study, Final Project Requirements and RAD Report Template are unavailable in the audited files.

## Evidence and coverage

| Use case | Evidence in repository | Model contribution | Status |
|---|---|---|---|
| UC03 Place Order | Placeholder directory only; existing shared flow and UC07 precondition say an Order enters Pending after checkout. | Customer, Order, OrderLine, MenuItem, Hub; initial Pending. | Proposed pending Khang's specification. |
| UC04 Track Order | Placeholder directory only; UC07 and UC10 state that Customer sees updates through UC04. | Reads Order.status; no state change. | Proposed pending Khang's specification. |
| UC07 Confirm/Reject Order | UC07 description and Thành's domain/state diagrams. | Pending to Confirmed or Rejected; rejectionReason. | Team draft; role/assumptions require confirmation. |
| UC10 Deliver Order | UC10 description and Thành's domain/state diagrams. | Ready to OutForDelivery, then Delivered or Failed; Shipper, cashCollected, failureReason. | Team draft; COD and assignment rules require confirmation. |
| UC13 Manage Hubs and Kitchen Capacity | Tài's UC13 draft; no Case Study source. | Hub.capacitySetting; no direct Order state change. | Proposed; UC13/UC14 ownership conflict. |
| UC16 Produce Management Reports | Tài's UC16 draft and workbook Q5/A-05. | Derived ManagementReport reads Order and Hub concepts. | Proposed; KPI/period/access unconfirmed. |

UC08 Prepare Order and UC05 Cancel/Edit Order are included only as transitions required to connect the six reviewed use cases with Thành's existing Order state machine. Their detailed specifications are outside this model's source set.

## Domain classes and attributes

| Class | Attributes | Basis / decision |
|---|---|---|
| Customer | `customerId` | Existing UC07/UC10 domain model. |
| Hub | `hubId`; `name`, `capacitySetting` proposed | Existing hub identity; UC13 requests capacity management but does not define unit or bounds. |
| Brand | `brandId`, `name` proposed | Proposal and workbook mention brand/menu browsing and UC14, but no approved specification is present. |
| MenuItem | `menuItemId`; `name`, `currentPrice` proposed | Existing menu item identity; browsing and order line pricing imply candidate descriptive fields. |
| Order | `id`, `status`, `paymentMethod`, `totalDue`, optional `rejectionReason`, `failureReason`, `cashCollected`; `placedAt` proposed | Core fields from Thành's model. `placedAt` is a candidate for report periods and awaits definition. |
| OrderLine | `quantity`, `unitPrice` | Existing model; `unitPrice` is the price recorded with the order line, not a claim about price-update policy. |
| Shipper | `shipperId` | Existing model. |
| ManagementReport | `reportType`, `period`, `scope`, `dataStatus` proposed | Derived business result for UC16; persistence is not confirmed. |

No boundary, controller, repository or other software-layer class is included in the domain diagram.

## Associations, multiplicities and constraints

| Relationship | Multiplicity | Business meaning / evidence |
|---|---|---|
| Customer places Order | Customer `1` to Order `0..*`; each Order has `1` Customer. | Preserved from Thành's domain model. |
| Hub fulfils Order | Hub `1` to Order `0..*`; each Order has `1` Hub. | Preserved from Thành's domain model; reassignment after overload remains To Confirm. |
| Shipper assigned to Order | Order has `0..1` current Shipper; Shipper may have `0..*` Orders. | Preserved from Thành's domain model; assignment policy remains To Confirm. |
| Order contains OrderLine | Order `1` composition to `1..*` OrderLines. | Preserved from Thành's domain model; order editing policy remains To Confirm. |
| OrderLine refers to MenuItem | Each OrderLine refers to `1` MenuItem; a MenuItem may appear in `0..*` OrderLines. | Preserved from Thành's domain model. |
| Brand groups MenuItem | Each MenuItem has `1` Brand; a Brand has `0..*` MenuItems. | **Proposed / To Confirm**; no UC03/UC04 specification validates this cardinality. |
| Hub offers MenuItem | Not encoded until cardinality is known. | **To Confirm**; hub-specific availability and an association class may be needed once requirements arrive. |
| ManagementReport derives values from Order and Hub | Dependencies, not persistent associations. | **Proposed / To Confirm**; source records and formulas await Q5 answer. |

Constraints requiring confirmation: hub capacity unit/bounds/effective time; hub deletion and order retention; menu availability by hub; pricing snapshot rules; order cancellation cutoff; role and hub-scoped authorization; shipper assignment; COD evidence; report KPI inclusion rules, reporting period/timezone and data visibility. The model does not encode these as approved invariants.

## Order lifecycle consistency

`Pending` follows a valid UC03 checkout in the existing team flow. UC07 can move `Pending` to `Confirmed` or `Rejected`. UC08 bridges `Confirmed` through `Preparing` to `Ready`. UC10 moves `Ready` to `OutForDelivery`, then to either `Delivered` or `Failed`. Thành's diagram also allows `Pending` to `Cancelled` via UC05. UC04 observes state; UC13 maintains Hub data; UC16 derives read-only reports. Terminal states have no outgoing business transition in the current draft.

The state names and transitions are consistent with the available UC07/UC10 drafts and Thành's state diagram. Because UC03/UC04 and the official Case Study are absent, initial state, cancellation eligibility, terminal-state policy and any additional states remain **To Confirm**.
