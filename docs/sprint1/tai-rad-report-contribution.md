# SaigonBite RAD Report — Võ Tấn Tài Contribution (Draft)

**Student:** Võ Tấn Tài — 524H0126
**Team:** F4
**Coverage:** UC13 Manage Hubs and Kitchen Capacity; UC16 Produce Management Reports; overall domain class model; Order state machine.
**Status:** Independent contribution for later integration. It is **not** the official RAD report: the SaigonBite Case Study, Final Project Requirements and RAD Report Template were unavailable in the audited repository and supplied files.

## Proposed placement in RAD Report Sections I–III

| Report section | Contribution to integrate | Evidence / required team action |
|---|---|---|
| I. Business Requirements | State that hub management/capacity and management reporting are candidate business capabilities. Record Q1/A-01 for hub overload and Q5/A-05 for report metrics as open assumptions. Identify UC13 versus UC14 ownership conflict. | Team Workbook Client Q&A and Assumption Log; proposal. Do not mark client approval without lecturer response. |
| II. System Requirements Analysis | Include UC13 and UC16 use case descriptions, Activity and SSD figures; overall domain model and Order state machine; the six-UC consistency and multiplicity notes below. | UC13/UC16 drafts and shared model source files. Confirm UC03/UC04 with Khang and UC07/UC10 with Thành. |
| III. System Requirements Design | Include UC13 and UC16 boundary/controller/domain/data-access classes, design class diagrams, CRC cards, UC13 CRUD verification and UC16 report logic review. | Design documents and PNG figures listed below. Confirm policies before final design approval. |

The official template may use different numbering or captions. Transfer content only after obtaining it and preserving its headings and instructions.

## Section I contribution — business context and open decisions

SaigonBite is a proposed cloud-kitchen ordering and delivery system. The team proposal identifies overloaded hubs, order delays and management visibility as problems. UC13 addresses maintenance of hub and kitchen capacity information. UC16 addresses managers' access to operational reports. These capabilities depend on reliable order, hub and delivery records, but the available material does not define capacity units, overload policy, reporting formulas or data access limits.

The Part 1 proposal and Team Workbook assign this student UC14 (brand/menu management) and UC16, while the current task and repository placeholder identify UC13 and UC16. The team must resolve that conflict before the final ownership table and scope statement are submitted. Q1/A-01 proposes customer approval before using an alternative hub; Q5/A-05 proposes sales, hub workload and delivery reports by day/week. Both remain unconfirmed. No business rule in this contribution treats those proposals as client-approved.

## Section II contribution — analysis model

### UC13 Manage Hubs and Kitchen Capacity

The [UC13 use case specification](UC13_ManageHubs/UC13.md) describes the candidate Admin actor, Create/Read/Update/Delete results, validation, authorization, conflict and removal-block cases. The actor, capacity semantics and delete/archive policy are Proposed / To Confirm.

**UC13 Activity diagram — purpose:** Show the decision path from opening hub management to each CRUD outcome. **Main components:** Admin and System swimlanes, operation switch, authorization and validation decisions, success/error responses. **Business meaning:** Hub records should change only after the applicable checks; failures preserve the prior record. **Related use case:** UC13; hub selection during UC03 is separate and remains unconfirmed.

**UC13 SSD — purpose:** Identify actor-to-system events for hub CRUD without exposing internal classes. **Main components:** `listHubs`, `createHub`, `getHub`, `updateHub`, `removeHub`, with alternate success/error responses. **Business meaning:** Each operation has an observable result; concurrent edits and removal policy need confirmation. **Related use case:** UC13.

### UC16 Produce Management Reports

The [UC16 use case specification](UC16_ManagementReports/UC16.md) describes a Manager requesting an authorized report by type, period and scope. Sales, hub workload and delivery performance are candidate categories; KPI formulas and period rules await Q5.

**UC16 Activity diagram — purpose:** Show authorization, filter checks, retrieval, aggregation and data-quality decisions. **Main components:** Manager and System swimlanes; no-data, incomplete-data and failure paths. **Business meaning:** The system should distinguish a complete result from missing or unreliable data without changing operational records. **Related use case:** UC16, using records associated with UC03, UC10 and UC13.

**UC16 SSD — purpose:** Identify `listAvailableReports` and `produceReport` as system events and show alternate responses. **Main components:** Manager, SaigonBite System, access denial, invalid filter, no-data, incomplete and successful result branches. **Business meaning:** Only an authorized scope can be queried; report context must accompany values. **Related use case:** UC16.

### Overall domain class model

**Purpose:** Bring order placement/tracking, kitchen decision, delivery, hub management and reporting into one conceptual vocabulary. **Main components:** `Customer`, `Order`, `OrderLine`, `MenuItem`, `Hub`, `Shipper`, proposed `Brand`, and a derived proposed `ManagementReport`. **Business meaning:** A customer places orders; an order belongs to one hub, contains order lines and may have a current shipper; hub capacity is business data, while a management report is derived rather than a confirmed persistent record. **Related use cases:** UC03, UC04, UC07, UC10, UC13 and UC16. The [model notes](shared/domain-model/06-overall-model-notes.md) record attributes, multiplicities and their evidence. No UI, controller or repository class appears in this diagram.

The five core associations and multiplicities match Thành's existing UC07/UC10 model. Brand-to-MenuItem (`1` to `0..*`) is proposed. Hub-to-MenuItem availability is left unencoded until its cardinality is known. `placedAt`, hub capacity details and report attributes are also proposed. No model attribute is presented as a confirmed requirement when its source is absent.

### Order state machine

**Purpose:** Check that the Order lifecycle agrees with placement, kitchen confirmation/preparation and delivery. **Main components:** `Pending`, `Confirmed`, `Rejected`, `Cancelled`, `Preparing`, `Ready`, `OutForDelivery`, `Delivered` and `Failed`, with event labels and guards. **Business meaning:** UC07 decides a Pending order; UC08 prepares it; UC10 records pickup and final delivery result. UC04 observes state, UC13 manages Hub data and UC16 reads data without moving the Order. **Related use cases:** UC03, UC04, UC07, UC10, UC13 and UC16, with UC05/UC08 shown as necessary neighbouring transitions. The model follows Thành's state diagram without overwriting it. Initial checkout state, cancellation eligibility and full status policy remain To Confirm.

## Section III contribution — design model

**UC13 design class diagram — purpose:** Allocate CRUD responsibilities across `HubManagementView`, `HubManagementController`, `Hub`, access/removal policies and `HubRepository`. **Main components:** attributes, public methods, private fields and associations between boundary, controller, domain and data access layers. **Business meaning:** Permission and removal decisions are explicit, and persistence failures can be reported without assuming a hard-delete rule. **Related use case:** UC13. The [UC13 design document](UC13_ManageHubs/UC13-design.md) supplies CRC cards and an operation-by-operation CRUD table.

**UC16 design class diagram — purpose:** Allocate access checks, definition lookup, source reads, aggregation and presentation. **Main components:** `ManagementReportView`, `ManagementReportController`, access policy, definition/catalogue, read-only source, aggregator and report result. **Business meaning:** An undefined KPI cannot be silently calculated, and an incomplete result cannot be presented as complete. **Related use case:** UC16. The [UC16 design document](UC16_ManagementReports/UC16-design.md) supplies CRC cards and checks for access, filters, no-data, incomplete data, errors and concurrency.

The two design diagrams include software-layer classes; the overall domain class diagram deliberately does not. Implementing a backend or database schema is outside this contribution.

## Figure register for Word and PowerPoint

The identifiers below are provisional; renumber according to the official report template. Each PNG was rendered from its adjacent editable `.puml` source.

| ID | Caption | PNG to insert | Suggested placement |
|---|---|---|---|
| T-F1 | UC13 Activity Diagram — hub and kitchen capacity CRUD with error paths | `UC13_ManageHubs/diagrams/13-activity.png` | Section II |
| T-F2 | UC13 System Sequence Diagram — hub CRUD events and responses | `UC13_ManageHubs/diagrams/13-ssd.png` | Section II |
| T-F3 | UC16 Activity Diagram — report access, aggregation and data-quality paths | `UC16_ManagementReports/diagrams/16-activity.png` | Section II |
| T-F4 | UC16 System Sequence Diagram — report request and alternate results | `UC16_ManagementReports/diagrams/16-ssd.png` | Section II |
| T-F5 | Overall Domain Class Model — six-use-case conceptual integration (Proposed) | `shared/domain-model/06-overall-domain.png` | Section II |
| T-F6 | Order State Machine — placement through delivery (Proposed) | `shared/domain-model/07-overall-order-state.png` | Section II |
| T-F7 | UC13 Design Class Diagram — boundary, controller, domain and data access | `UC13_ManageHubs/diagrams/13-design-class.png` | Section III |
| T-F8 | UC16 Design Class Diagram — reporting boundary, controller, domain and read access | `UC16_ManagementReports/diagrams/16-design-class.png` | Section III |

For PowerPoint, use the same captions in shortened form and keep “Proposed” visible on figures T-F5/T-F6. Figure source paths above are relative to `docs/sprint1/`.

## Integration checks and unresolved items

| Check | Result / required follow-up |
|---|---|
| UC03 and UC04 files | Only placeholders exist in the repository. Verify Order creation, tracking permissions and catalogue relationships when Khang's specifications arrive. |
| UC07 and UC10 | The Order lifecycle and core domain associations follow Thành's drafts. Their cited assumptions remain team drafts, not client approvals. |
| UC13 versus UC14 | Proposal and workbook assign UC14; current task assigns UC13. Team must approve the ownership and scope change. |
| Capacity and overload | Units, bounds, effective time, routing and customer consent remain open. |
| Report metrics | KPI formulas, inclusion rules, period/timezone, access scope and data-quality policy remain open under Q5/A-05. |
| Figure quality | PlantUML syntax and PNG rendering were checked; final report pagination and caption numbering await the official template. |

**Do not mark this contribution or the workbook as Client Approved until the lecturer/client answers are recorded.**
