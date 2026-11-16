# Overall Domain and Order State Model — Review Notes

**Author:** Võ Tấn Tài — 524H0126
**AI use:** AI-assisted draft; student review is required before submission. See the Team Workbook AI Usage Log.

**Status:** Proposed integration model for UC03, UC04, UC07, UC10, UC13 and UC16. This does not replace the UC07/UC10 diagrams by Lê Đỗ Minh Thành. The official [Case Study, Final Project Requirements and Report Template](https://drive.google.com/drive/folders/14cJnJ9_AhfFeWIxvzuRefNueToF5RyNF) were supplied during the 03 November 2026 update review. UC03/UC04 files were copied unchanged from `origin/feature/khang-uc03-uc04` into Tài's branch for integration review; Khang's branch itself was not changed.

## Evidence and coverage

| Use case | Evidence in repository | Model contribution | Status |
|---|---|---|---|
| UC03 Place Order | Khang's copied draft specifies COD as `PENDING_CONFIRMATION`, online as `AWAITING_PAYMENT`, plus order/address/price snapshots. | Customer, Order, OrderLine, MenuItem, Hub; proposed payment status and online waiting state. | Source integrated; vocabulary not team reconciled. |
| UC04 Track Order | Khang's copied draft specifies ownership-scoped read, milestones and timestamps. | Reads Order.status and proposed OrderMilestone; no state change. | Source integrated; vocabulary not team reconciled. |
| UC07 Confirm/Reject Order | UC07 description and Thành's domain/state diagrams. | Pending to Confirmed or Rejected; rejectionReason. | Team draft; role/assumptions require confirmation. |
| UC10 Deliver Order | UC10 description and Thành's domain/state diagrams. | Ready to OutForDelivery, then Delivered or Failed; Shipper, cashCollected, failureReason. | Team draft; COD and assignment rules require confirmation. |
| UC13 Manage Hubs and Kitchen Capacity | Official Case Study and Final Project Requirements identify Admin maintenance and limited hub capacity; Tài's UC13 draft. | Hub.capacitySetting; no direct Order state change. | UC13 is a source-backed candidate; UC13/UC14 team ownership conflict and capacity details remain open. |
| UC16 Produce Management Reports | Official Case Study and Final Project Requirements name Manager and sales, hub workload and delivery performance; workbook Q5/A-05 is still unanswered. | Derived ManagementReport reads Order and Hub concepts. | Categories confirmed; KPI/period/access unconfirmed. |

UC08 Prepare Order and UC05 Cancel/Edit Order are included only as transitions required to connect the six reviewed use cases with Thành's existing Order state machine. Their detailed specifications are outside this model's source set.

## Domain classes and attributes

| Class | Attributes | Basis / decision |
|---|---|---|
| Customer | `customerId` | Existing UC07/UC10 domain model; generalizes the Case Study's two customer types. |
| LocalCustomer | `mobileNumber` | The Case Study specifies Vietnamese mobile registration for local customers. |
| TouristCustomer | `passportDetails`, `emailAddress` | The Case Study specifies passport details and email registration for foreign tourists. Privacy handling remains to be designed. |
| Hub | `hubId`; `name` proposed; `capacitySetting` confirmed as a concept, with unit/threshold To Confirm | Existing hub identity and Case Study capacity constraint. |
| Brand | `brandId`, `name` proposed | The Case Study confirms virtual brands and that each hub works with several; exact identifiers and naming fields are proposed. |
| Voucher | `voucherId` proposed | The Case Study confirms vouchers and at most one voucher per order; identifier is proposed. |
| MenuItem | `menuItemId`; `name`, `currentPrice` proposed | Existing menu item identity; browsing and order line pricing imply candidate descriptive fields. |
| Order | `id`, `status`, `paymentMethod`, `totalDue`, optional `rejectionReason`, `failureReason`, `cashCollected`; `paymentStatus`, `deliveryAddressSnapshot`, `clientRequestId`, `placedAt`, `updatedAt` proposed | Core fields from Thành's model; added fields are proposed from Khang's UC03/UC04 drafts on a separate branch. |
| OrderLine | `quantity`, `unitPrice`; `nameSnapshot` proposed | Existing quantity and unit price; Khang's draft proposes a name snapshot. |
| OrderMilestone | `status`, `occurredAt` proposed | Khang's UC04 tracking draft uses milestones; persistence and source of timestamps need confirmation. |
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
| Order records OrderMilestone | Order `1` composition to `0..*` proposed milestones. | **Proposed / To Confirm** from Khang's UC04 draft; event storage and lifecycle need agreement. |
| OrderLine refers to MenuItem | Each OrderLine refers to `1` MenuItem; a MenuItem may appear in `0..*` OrderLines. | Preserved from Thành's domain model. |
| Brand groups MenuItem | Each MenuItem has `1` Brand; a Brand has `0..*` MenuItems. | **Proposed / To Confirm**; the Case Study mentions brands and menus but not this exact cardinality. |
| Hub works with Brand | Each Hub works with `1..*` Brands; a Brand may work with `0..*` Hubs. | The Case Study confirms several brands per Hub. Brand-to-Hub reuse and exact minimum remain **Proposed / To Confirm**. |
| Order applies Voucher | An Order has `0..1` Voucher; a Voucher may apply to `0..*` Orders. | At most one voucher per Order is a Case Study fact. Voucher reuse cardinality remains **Proposed / To Confirm**. |
| Hub offers MenuItem | Not encoded until cardinality is known. | **To Confirm**; hub-specific availability and an association class may be needed once requirements arrive. |
| ManagementReport derives values from Order and Hub | Dependencies, not persistent associations. | **Proposed / To Confirm**; source records and formulas await Q5 answer. |

The Case Study also fixes that hubs cook only for delivery, a busy hub stops taking new orders, quieter hubs are encouraged, delivery has a maximum distance and a distance-based fee, and an order eventually reaches delivery, cancellation or failure. The exact busy rule, incentive, distance, fees and discounts still need client detail. Constraints requiring confirmation: hub capacity unit/bounds/effective time; hub deletion and order retention; menu availability by hub; pricing snapshot rules; order cancellation cutoff; role and hub-scoped authorization; shipper assignment; COD evidence; report KPI inclusion rules, reporting period/timezone and data visibility. The model does not encode these as approved invariants.

## Order lifecycle consistency

The revised proposed state model shows COD placement into `Pending` and online placement into `AwaitingPayment`. The latter moves to `Pending` only after a verified payment event, or to `Cancelled` on expiry. These online branches come from Khang's UC03 draft and are not yet accepted by the team. UC07 can move `Pending` to `Confirmed` or `Rejected`. UC08 bridges `Confirmed` through `Preparing` to `Ready`. UC10 moves `Ready` to `OutForDelivery`, then to either `Delivered` or `Failed`. Thành's diagram also allows `Pending` to `Cancelled` via UC05. UC04 observes state; UC13 maintains Hub data; UC16 derives read-only reports. Terminal states have no outgoing business transition in this draft.

The two team drafts conflict on state vocabulary and one outcome. Candidate name mappings are `Pending` ↔ `PENDING_CONFIRMATION`, `Confirmed` ↔ `ACCEPTED`, `Ready` ↔ `READY_FOR_PICKUP`, and `Failed` ↔ `DELIVERY_FAILED`. These are **not** approved mappings. Thành's UC07 uses `Rejected`, while Khang's Order lifecycle routes reject to `CANCELLED`; those outcomes cannot be treated as equivalent without a decision about reason, refund and tracking semantics. Khang's `AWAITING_PAYMENT` is absent from Thành's model. The Case Study confirms an order ends delivered, cancelled or failed but does not settle whether rejection is a separate persisted state. The team must settle the canonical status set, payment transitions, cancellation/expiry, capacity release and milestone source before integration. Cross-six consistency **FAILS between the current drafts**; the correct canonical resolution remains **NOT VERIFIED**.
