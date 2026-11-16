# SaigonBite RAD Report — Võ Tấn Tài Contribution (Draft)

**Student:** Võ Tấn Tài — 524H0126
**AI use:** AI-assisted draft; student review is required before submission. See the Team Workbook AI Usage Log.
**Team:** F4
**Coverage:** UC13 Manage Hubs and Kitchen Capacity; UC16 Produce Management Reports; overall domain class model; Order state machine.
**Status:** Independent contribution for later team integration, **not** the submitted team report. The official [Case Study, Final Project Requirements and RAD Report Template](https://drive.google.com/drive/folders/14cJnJ9_AhfFeWIxvzuRefNueToF5RyNF) were reviewed after the 03 November 2026 update. Open policies remain labelled **To Confirm**.

## Sprint 1 placement in the official report template

The template requires Sections I–III for Part 2. The team must preserve its real Word headings, numbering and author IDs, then export a bookmarked PDF. The mapping below identifies where Tài's existing contribution fits; it does not claim completion of the team report or lecturer approval.

| Template location | Tài contribution | Integration dependency |
|---|---|---|
| I 1.1, 1.3, 1.4 and 1.7 | Hub capacity and reporting business context; UC13/UC16 candidate stories, risks, assumptions and requirement statements. | Team must supply Part 1 approval record, prioritization, iteration plan and measurable NFRs. |
| II 2.1.5 | UC13 and UC16 ownership entries. | Resolve the Part 1 UC14 versus current UC13 assignment. |
| II 2.1.7 | Overall domain class model, attributes, multiplicities and provenance notes. | Reconcile Khang/Thành vocabulary and review proposed cardinalities. |
| II 2.2 | UC13 and UC16 descriptions, Activity diagrams and SSDs; UC13 Hub state machine as Tài's per-student lifecycle diagram. | Team assigns exact 2.2 subnumbers after fixing six-use-case order. |
| II 2.3 | UC13 Admin/Hub CRUD verification and UC16 read-only Manager/report coverage. | Team checks CRUD for every persistent class and actor in the whole portfolio. |
| III 3.x.1–3.x.5 | UC13/UC16 detailed classes, design class diagrams, CRC cards, OOD sequence diagrams and final integrated design class diagrams. | Team assigns exact 3.x use-case positions and reviews proposed result types. |

Team-owned I 1.2, 1.5 and 1.6, and II 2.1.1–2.1.6 require the team's charts, process models, narrative, event/actor lists and full use-case diagram. This contribution links to relevant models but does not fill those shared sections on behalf of other members.

## Business context and open decisions

SaigonBite is a proposed cloud-kitchen ordering and delivery system. The official Case Study identifies overloaded hubs, order delays and weak management visibility as problems. It states that busy hubs stop taking new orders and customers are encouraged to use quieter hubs. UC13 addresses maintenance of hub and kitchen capacity information; UC16 addresses managers' access to sales, hub workload and delivery performance reports. Capacity thresholds, incentive details, reporting formulas and data access limits still require confirmation.

The Part 1 proposal and Team Workbook assign this student UC14 (brand/menu management) and UC16, while the current task and repository placeholder identify UC13 and UC16. The team must resolve that conflict before the final ownership table and scope statement are submitted. Q1/A-01 proposes customer approval before using an alternative hub; Q5/A-05 proposes sales, hub workload and delivery reports by day/week. Both remain unconfirmed. No business rule in this contribution treats those proposals as client-approved.

## Use case and domain analysis

### UC13 Manage Hubs and Kitchen Capacity

The [UC13 use case specification](UC13_ManageHubs/UC13.md) describes the official candidate Admin actor, Create/Read/Update/Delete results, validation, authorization, conflict and removal-block cases. Capacity semantics, operation permissions and delete/archive policy are Proposed / To Confirm.

**UC13 Activity diagram — purpose:** Show the decision path from opening hub management to each CRUD outcome. **Main components:** Admin and System swimlanes, operation switch, authorization and validation decisions, success/error responses. **Business meaning:** Hub records should change only after the applicable checks; failures preserve the prior record. **Related use case:** UC13; hub selection during UC03 is separate.

**UC13 SSD — purpose:** Identify actor-to-system events for hub CRUD without exposing internal classes. **Main components:** `listHubs`, `createHub`, `getHub`, `updateHub`, `removeHub`, with alternate success/error responses. **Business meaning:** Each operation has an observable result; concurrent edits and removal policy need confirmation. **Related use case:** UC13.

**UC13 Hub state machine — purpose:** Tie the use case postconditions to one persistent domain object's lifecycle. **Main components:** recorded Hub, conditional archived/removed outcomes and internal Read/Update events. **Business meaning:** Read and failed writes preserve the record; the removal mode remains a client decision. **Related use case:** UC13.

### UC16 Produce Management Reports

The [UC16 use case specification](UC16_ManagementReports/UC16.md) describes a Manager requesting an authorized report by type, period and scope. Sales, hub workload and delivery performance are Case Study categories; KPI formulas and period rules await Q5.

**UC16 Activity diagram — purpose:** Show authorization, filter checks, retrieval, aggregation and data-quality decisions. **Main components:** Manager and System swimlanes; no-data, incomplete-data and failure paths. **Business meaning:** The system should distinguish a complete result from missing or unreliable data without changing operational records. **Related use case:** UC16, using records associated with UC03, UC10 and UC13.

**UC16 SSD — purpose:** Identify `listAvailableReports` and `produceReport` as system events and show alternate responses. **Main components:** Manager, SaigonBite System, access denial, invalid filter, no-data, incomplete and successful result branches. **Business meaning:** Only an authorized scope can be queried; report context must accompany values. **Related use case:** UC16.

### Overall domain class model

**Purpose:** Bring order placement/tracking, kitchen decision, delivery, hub management and reporting into one conceptual vocabulary. **Main components:** `Customer` with local/tourist specializations, `Order`, `OrderLine`, proposed `OrderMilestone`, `MenuItem`, `Hub`, `Shipper`, `Brand`, `Voucher`, and a derived proposed `ManagementReport`. **Business meaning:** A customer places orders; an order belongs to one hub, contains order lines, has at most one voucher and may have a current shipper. Hub capacity and brand relationships are shown, while a management report is derived rather than a confirmed persistent record. **Related use cases:** UC03, UC04, UC07, UC10, UC13 and UC16. The [model notes](shared/domain-model/06-overall-model-notes.md) record attributes, multiplicities and their evidence. No UI, controller or repository class appears in this diagram.

The five core associations and multiplicities match Thành's existing UC07/UC10 model. Local/tourist customer types and at most one voucher per order follow the Case Study. Brand-to-MenuItem (`1` to `0..*`), Voucher reuse and Order-to-OrderMilestone (`1` to `0..*`) are proposed. Hub-to-MenuItem availability is left unencoded until its cardinality is known. Added payment, address, timestamp, milestone and report attributes are proposed from the available drafts. Capacity is a confirmed concept; its units and limits remain open.

### Order state machine

**Purpose:** Check the proposed Order lifecycle against placement, kitchen confirmation/preparation and delivery. **Main components:** `AwaitingPayment`, `Pending`, `Confirmed`, `Rejected`, `Cancelled`, `Preparing`, `Ready`, `OutForDelivery`, `Delivered` and `Failed`, with event labels and guards. **Business meaning:** Khang's UC03 draft adds an online-payment waiting path; UC07 decides a Pending order; UC08 prepares it; UC10 records pickup and final delivery result. UC04 observes state, UC13 manages Hub data and UC16 reads data without moving the Order. **Related use cases:** UC03, UC04, UC07, UC10, UC13 and UC16, with UC05/UC08 and supporting payment shown as neighbouring transitions. Thành's status names are retained for the fulfilment path, while Khang's different labels and rejection outcome require team reconciliation. The figure is not a canonical state contract.

## Design model

**UC13 design class diagram — purpose:** Allocate CRUD responsibilities across `HubManagementView`, `HubManagementController`, `Hub`, access/removal policies and `HubRepository`. **Main components:** attributes, public methods, private fields and associations between boundary, controller, domain and data access layers. **Business meaning:** Permission and removal decisions are explicit, and persistence failures can be reported without assuming a hard-delete rule. **Related use case:** UC13. The [UC13 design document](UC13_ManageHubs/UC13-design.md) supplies CRC cards and an operation-by-operation CRUD table.

**UC13 OOD sequence and final class diagrams — purpose:** Trace the CRUD collaboration and consolidate the result contract after sequence review. **Main components:** View, Controller, policies, Hub, Repository and a proposed `HubOperationResult`. **Business meaning:** Each authorized path produces a success or explicit error without silently assuming deletion semantics. **Related use case:** UC13.

**UC16 design class diagram — purpose:** Allocate access checks, definition lookup, source reads, aggregation and presentation. **Main components:** `ManagementReportView`, `ManagementReportController`, access policy, definition/catalogue, read-only source, aggregator and report result. **Business meaning:** An undefined KPI cannot be silently calculated, and an incomplete result cannot be presented as complete. **Related use case:** UC16. The [UC16 design document](UC16_ManagementReports/UC16-design.md) supplies CRC cards and checks for access, filters, no-data, incomplete data, errors and concurrency.

**UC16 OOD sequence and final class diagrams — purpose:** Trace authorization, report definition, source quality and aggregation into an explicit result contract. **Main components:** View, Controller, access policy, catalogue, definition, read-only repository, aggregator, `ManagementReport` and proposed `ReportResult`. **Business meaning:** A missing definition, empty source and processing error remain distinguishable. **Related use case:** UC16.

The design diagrams include software-layer classes; the overall domain class diagram deliberately does not. The latest Final Project Requirements contain both Sprint 2 implementation/running-system requirements and a later sentence saying "No coding needed". The team should obtain lecturer clarification before treating either interpretation as approved; no application code is added in Sprint 1.

## Figure register for Word and PowerPoint

The identifiers below are provisional; renumber after the team fixes the six-use-case order in the official template. Each PNG was rendered from its adjacent editable `.puml` source.

| ID | Caption | PNG to insert | Report placement |
|---|---|---|---|
| T-F1 | UC13 Activity Diagram — hub and kitchen capacity CRUD with error paths | `UC13_ManageHubs/diagrams/13-activity.png` | II 2.2, UC13 entry |
| T-F2 | UC13 System Sequence Diagram — hub CRUD events and responses | `UC13_ManageHubs/diagrams/13-ssd.png` | II 2.2, UC13 entry |
| T-F3 | UC13 Hub State Machine — record lifecycle and conditional removal (Proposed) | `UC13_ManageHubs/diagrams/13-hub-state.png` | II 2.2, UC13 entry |
| T-F4 | UC16 Activity Diagram — report access, aggregation and data-quality paths | `UC16_ManagementReports/diagrams/16-activity.png` | II 2.2, UC16 entry |
| T-F5 | UC16 System Sequence Diagram — report request and alternate results | `UC16_ManagementReports/diagrams/16-ssd.png` | II 2.2, UC16 entry |
| T-F6 | Overall Domain Class Model — six-use-case conceptual integration (Proposed) | `shared/domain-model/06-overall-domain.png` | II 2.1.7 |
| T-F7 | Order State Machine — placement through delivery (Proposed) | `shared/domain-model/07-overall-order-state.png` | Shared lifecycle cross-check; place after team review |
| T-F8 | UC13 Design Class Diagram — boundary, controller, domain and data access | `UC13_ManageHubs/diagrams/13-design-class.png` | III, UC13 entry |
| T-F9 | UC13 OOD Sequence Diagram — CRUD class collaboration (Proposed) | `UC13_ManageHubs/diagrams/13-ood-sequence.png` | III, UC13 entry |
| T-F10 | UC13 Final Integrated Design Class Diagram (Proposed) | `UC13_ManageHubs/diagrams/13-final-design-class.png` | III, UC13 entry |
| T-F11 | UC16 Design Class Diagram — reporting boundary, controller, domain and read access | `UC16_ManagementReports/diagrams/16-design-class.png` | III, UC16 entry |
| T-F12 | UC16 OOD Sequence Diagram — report class collaboration (Proposed) | `UC16_ManagementReports/diagrams/16-ood-sequence.png` | III, UC16 entry |
| T-F13 | UC16 Final Integrated Design Class Diagram (Proposed) | `UC16_ManagementReports/diagrams/16-final-design-class.png` | III, UC16 entry |

For PowerPoint, use the same captions in shortened form and keep “Proposed” visible on integration and policy-dependent diagrams. Figure source paths above are relative to `docs/sprint1/`.

## Integration checks and unresolved items

| Check | Result / required follow-up |
|---|---|
| UC03 and UC04 files | This branch has placeholders. Khang's draft specifications and diagrams are on `origin/feature/khang-uc03-uc04`; they were reviewed without merging. Integrate only after team review. |
| UC07 and UC10 | The Order lifecycle and core domain associations follow Thành's drafts. Their cited assumptions remain team drafts, not client approvals. |
| UC13 versus UC14 | Proposal and workbook assign UC14; current task assigns UC13. Team must approve the ownership and scope change. |
| Capacity and overload | Units, bounds, effective time, routing and customer consent remain open. |
| Order status vocabulary | Khang uses `PENDING_CONFIRMATION`, `ACCEPTED`, `READY_FOR_PICKUP`, `DELIVERY_FAILED` and `AWAITING_PAYMENT`; Thành uses `Pending`, `Confirmed`, `Ready`, `Failed` and a separate `Rejected`. Rejection versus cancellation and online payment require an explicit decision. |
| Report metrics | KPI formulas, inclusion rules, period/timezone, access scope and data-quality policy remain open under Q5/A-05. |
| Official sources | Case Study confirms UC13 Admin CRUD candidate and UC16 Manager/report categories. The 03 November 2026 template and requirements are available; detailed business decisions and a team submission still need review. |
| Sprint 2 implementation wording | Requirements pages 4, 6–7 and the template ask for a working system, SQL/code and a tagged release, while Requirements page 12 says "No coding needed". Obtain lecturer clarification; do not fabricate code or deployment evidence. |
| Figure quality | PlantUML syntax and PNG rendering were checked; final team report pagination, bookmarks and caption numbering remain unverified. |

**Do not mark this contribution or the workbook as Client Approved until the lecturer/client answers are recorded.**
