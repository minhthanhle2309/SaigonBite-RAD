# SaigonBite Sprint 1 Part 2 — Võ Tấn Tài Deliverables

## Project Overview

SaigonBite is Team F4's proposed cloud-kitchen ordering and delivery system. This folder is the entry point to Võ Tấn Tài's analysis and design contribution for UC13, UC16, the overall domain model and the Order state machine. These are editable Sprint 1 drafts for team review. They are not a client-approved system specification.

## Owner Information

- Student: Võ Tấn Tài
- Student ID: 524H0126
- Working branch: `feature/tai-uc13-uc16`
- Scope: UC13 Manage Hubs and Kitchen Capacity; UC16 Produce Management Reports; overall domain and Order lifecycle models; report integration draft; workbook contribution.

## UC13

The [use case description](../UC13_ManageHubs/UC13.md) covers goal, actor, preconditions, postconditions, the Create main scenario, Read/Update/Delete alternatives, errors and proposed rules. The [design document](../UC13_ManageHubs/UC13-design.md) contains boundary, controller, domain and data-access classes, CRC cards and CRUD verification. The diagram sources and PNGs are in `docs/sprint1/UC13_ManageHubs/diagrams/`:

| Diagram | Editable source | Rendered image |
|---|---|---|
| Activity | [13-activity.puml](../UC13_ManageHubs/diagrams/13-activity.puml) | [13-activity.png](../UC13_ManageHubs/diagrams/13-activity.png) |
| System Sequence Diagram | [13-ssd.puml](../UC13_ManageHubs/diagrams/13-ssd.puml) | [13-ssd.png](../UC13_ManageHubs/diagrams/13-ssd.png) |
| Design Class Diagram | [13-design-class.puml](../UC13_ManageHubs/diagrams/13-design-class.puml) | [13-design-class.png](../UC13_ManageHubs/diagrams/13-design-class.png) |

The actor, capacity units/limits and hub removal policy remain **Proposed / To Confirm**. The proposal/workbook originally assigned UC14 brand/menu management to this student, so UC13 ownership needs a team decision.

## UC16

The [use case description](../UC16_ManagementReports/UC16.md) covers an authorized Manager's report request, filters, results and failure paths. The [design document](../UC16_ManagementReports/UC16-design.md) contains classes, CRC cards and checks for permission, data quality and aggregation. Diagram sources and PNGs are in `docs/sprint1/UC16_ManagementReports/diagrams/`:

| Diagram | Editable source | Rendered image |
|---|---|---|
| Activity | [16-activity.puml](../UC16_ManagementReports/diagrams/16-activity.puml) | [16-activity.png](../UC16_ManagementReports/diagrams/16-activity.png) |
| System Sequence Diagram | [16-ssd.puml](../UC16_ManagementReports/diagrams/16-ssd.puml) | [16-ssd.png](../UC16_ManagementReports/diagrams/16-ssd.png) |
| Design Class Diagram | [16-design-class.puml](../UC16_ManagementReports/diagrams/16-design-class.puml) | [16-design-class.png](../UC16_ManagementReports/diagrams/16-design-class.png) |

Sales, hub workload and delivery performance are candidate categories. KPI formulas, periods, scope permissions and completeness rules remain **To Confirm** under workbook Q5/A-05.

## Domain Class Model

The [overall domain source](../shared/domain-model/06-overall-domain.puml) and [PNG](../shared/domain-model/06-overall-domain.png) cover Customer, Order, OrderLine, Hub, Shipper, MenuItem and proposed Brand, OrderMilestone and derived ManagementReport concepts. The [model notes](../shared/domain-model/06-overall-model-notes.md) list attributes, associations, multiplicities, constraints and evidence. The diagram contains domain concepts only; no View, Controller or Repository class appears in it.

Five core associations are preserved from Thành's UC07/UC10 diagram. Additional attributes/milestones draw on Khang's UC03/UC04 drafts on `origin/feature/khang-uc03-uc04`, which were read without merging. Candidate cardinalities are labelled Proposed and require team review.

## State Machine

The [Order state source](../shared/domain-model/07-overall-order-state.puml) and [PNG](../shared/domain-model/07-overall-order-state.png) show placement, confirmation/rejection, preparation, pickup, delivery and failure. A proposed online-payment waiting branch comes from Khang's draft. This is **not yet a canonical team state contract**: Khang and Thành use different status names, and Khang routes rejection to `CANCELLED` while Thành uses `Rejected`. The [model notes](../shared/domain-model/06-overall-model-notes.md) record the discrepancy and decisions needed.

## Documentation Structure

- `docs/sprint1/UC13_ManageHubs/`: UC13 specification, design/CRC/CRUD document, `.puml` sources and `.png` images.
- `docs/sprint1/UC16_ManagementReports/`: UC16 specification, design/CRC document, `.puml` sources and `.png` images.
- `docs/sprint1/shared/domain-model/06-overall-*` and `07-overall-order-state.*`: Tài's integration models; Thành's `04-domain.*` and `05-order-state.*` remain separate.
- [RAD report contribution](../tai-rad-report-contribution.md): Sections I–III draft, diagram explanations and eight figure captions for Word/PowerPoint.
- `references/TeamF4_RAD_Team_Workbook_Part1.xlsx`: updated team workbook copy; the original file outside the repository remains untouched.
- [Final checklist](../../../TAI_FINAL_CHECKLIST.md): requirement-by-requirement PASS, FAIL and NOT VERIFIED evidence.

## UML Rendering Instructions

Install Java and obtain a PlantUML JAR. From the repository root, replace `<plantuml.jar>` with its local path and run the commands below for any source file. PNGs are written beside the `.puml` source.

```text
java -jar <plantuml.jar> -charset UTF-8 -checkonly docs/sprint1/UC13_ManageHubs/diagrams/13-activity.puml
java -jar <plantuml.jar> -charset UTF-8 -tpng docs/sprint1/UC13_ManageHubs/diagrams/13-activity.puml
```

Repeat for the eight `.puml` files linked above. The final QA used PlantUML `1.2026.10`; every PNG was regenerated and compared with its editable source.

## Deliverables and Verification Results

Eight PlantUML sources have matching rendered PNGs. Syntax checking and image inspection passed for the eight diagrams. UC13/UC16 descriptions, design documents, CRC cards and report links were checked against their diagrams. The workbook retained 13 sheets and its formulas; only Tài-owned content was edited. Exact evidence and remaining issues are in the [final checklist](../../../TAI_FINAL_CHECKLIST.md).

## Known Limitations

- The original SaigonBite Case Study, Final Project Requirements and official RAD Report Template were unavailable. The report contribution is an independent draft, not the official completed report.
- UC13 versus UC14 ownership must be settled by Team F4. Capacity, hub removal, report KPI/period and access policies await a client/lecturer answer.
- UC03/UC04 drafts are on Khang's separate branch and have not been merged. Their Order status names and rejection outcome conflict with Thành's drafts. The current cross-six state consistency check **fails**; a shared status contract remains unverified.
- The workbook commit count is a dated snapshot through `af1fa21`; Git history is the authoritative count after this final review commit.
