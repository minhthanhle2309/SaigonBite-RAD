# SaigonBite Sprint 1 Part 2 — Võ Tấn Tài Deliverables

## Project Overview

SaigonBite is Team F4's proposed cloud-kitchen ordering and delivery system. This folder is the entry point to Võ Tấn Tài's analysis and design contribution for UC13, UC16, the overall domain model and the Order state machine. These are editable Sprint 1 drafts for team review. They are not a client-approved system specification.

## Owner Information

- Student: Võ Tấn Tài
- Student ID: 524H0126
- Working branch: `feature/tai-uc13-uc16`
- Scope: UC13 Manage Hubs and Kitchen Capacity; UC16 Produce Management Reports; overall domain and Order lifecycle models; report integration draft; workbook contribution.
- AI use: these are AI-assisted drafts; student review is required before submission and the workbook AI Usage Log records the assistance.

## UC13

The [use case description](../UC13_ManageHubs/UC13.md) covers goal, actor, preconditions, postconditions, the Create main scenario, Read/Update/Delete alternatives, errors and proposed rules. The [design document](../UC13_ManageHubs/UC13-design.md) contains boundary, controller, domain and data-access classes, CRC cards and CRUD verification. The diagram sources and PNGs are in `docs/sprint1/UC13_ManageHubs/diagrams/`:

| Diagram | Editable source | Rendered image |
|---|---|---|
| Activity | [13-activity.puml](../UC13_ManageHubs/diagrams/13-activity.puml) | [13-activity.png](../UC13_ManageHubs/diagrams/13-activity.png) |
| System Sequence Diagram | [13-ssd.puml](../UC13_ManageHubs/diagrams/13-ssd.puml) | [13-ssd.png](../UC13_ManageHubs/diagrams/13-ssd.png) |
| Design Class Diagram | [13-design-class.puml](../UC13_ManageHubs/diagrams/13-design-class.puml) | [13-design-class.png](../UC13_ManageHubs/diagrams/13-design-class.png) |
| Hub State Machine | [13-hub-state.puml](../UC13_ManageHubs/diagrams/13-hub-state.puml) | [13-hub-state.png](../UC13_ManageHubs/diagrams/13-hub-state.png) |
| OOD Sequence Diagram | [13-ood-sequence.puml](../UC13_ManageHubs/diagrams/13-ood-sequence.puml) | [13-ood-sequence.png](../UC13_ManageHubs/diagrams/13-ood-sequence.png) |
| Final Design Class Diagram | [13-final-design-class.puml](../UC13_ManageHubs/diagrams/13-final-design-class.puml) | [13-final-design-class.png](../UC13_ManageHubs/diagrams/13-final-design-class.png) |

The official Case Study/Final Project Requirements identify the Admin actor and limited hub capacity. Capacity units/limits and the removal policy remain **To Confirm**. The proposal/workbook originally assigned UC14 brand/menu management to this student, so UC13 ownership needs a team decision.

## UC16

The [use case description](../UC16_ManagementReports/UC16.md) covers an authorized Manager's report request, filters, results and failure paths. The [design document](../UC16_ManagementReports/UC16-design.md) contains classes, CRC cards and checks for permission, data quality and aggregation. Diagram sources and PNGs are in `docs/sprint1/UC16_ManagementReports/diagrams/`:

| Diagram | Editable source | Rendered image |
|---|---|---|
| Activity | [16-activity.puml](../UC16_ManagementReports/diagrams/16-activity.puml) | [16-activity.png](../UC16_ManagementReports/diagrams/16-activity.png) |
| System Sequence Diagram | [16-ssd.puml](../UC16_ManagementReports/diagrams/16-ssd.puml) | [16-ssd.png](../UC16_ManagementReports/diagrams/16-ssd.png) |
| Design Class Diagram | [16-design-class.puml](../UC16_ManagementReports/diagrams/16-design-class.puml) | [16-design-class.png](../UC16_ManagementReports/diagrams/16-design-class.png) |
| OOD Sequence Diagram | [16-ood-sequence.puml](../UC16_ManagementReports/diagrams/16-ood-sequence.puml) | [16-ood-sequence.png](../UC16_ManagementReports/diagrams/16-ood-sequence.png) |
| Final Design Class Diagram | [16-final-design-class.puml](../UC16_ManagementReports/diagrams/16-final-design-class.puml) | [16-final-design-class.png](../UC16_ManagementReports/diagrams/16-final-design-class.png) |

Sales, hub workload and delivery performance are Case Study categories. KPI formulas, periods, scope permissions and completeness rules remain **To Confirm** under workbook Q5/A-05.

## Domain Class Model

The [overall domain source](../shared/domain-model/06-overall-domain.puml) and [PNG](../shared/domain-model/06-overall-domain.png) cover Customer and its local/tourist types, Order, OrderLine, Hub, Shipper, MenuItem, Brand, Voucher, proposed OrderMilestone and derived ManagementReport. The [model notes](../shared/domain-model/06-overall-model-notes.md) list attributes, associations, multiplicities, constraints and evidence. The diagram contains domain concepts only; no View, Controller or Repository class appears in it.

Five core associations are preserved from Thành's UC07/UC10 diagram. Additional attributes/milestones draw on Khang's UC03/UC04 drafts on `origin/feature/khang-uc03-uc04`, which were read without merging. Candidate cardinalities are labelled Proposed and require team review.

## State Machine

The [Order state source](../shared/domain-model/07-overall-order-state.puml) and [PNG](../shared/domain-model/07-overall-order-state.png) show placement, confirmation/rejection, preparation, pickup, delivery and failure. A proposed online-payment waiting branch comes from Khang's draft. This is **not yet a canonical team state contract**: Khang and Thành use different status names, and Khang routes rejection to `CANCELLED` while Thành uses `Rejected`. The [model notes](../shared/domain-model/06-overall-model-notes.md) record the discrepancy and decisions needed.

## Documentation Structure

- `docs/sprint1/UC13_ManageHubs/`: UC13 specification, design/CRC/CRUD document, `.puml` sources and `.png` images.
- `docs/sprint1/UC16_ManagementReports/`: UC16 specification, design/CRC document, `.puml` sources and `.png` images.
- `docs/sprint1/shared/domain-model/06-overall-*` and `07-overall-order-state.*`: Tài's integration models; Thành's `04-domain.*` and `05-order-state.*` remain separate.
- [RAD report contribution](../tai-rad-report-contribution.md): exact Section I–III template mapping, diagram explanations and 13 figure captions for Word/PowerPoint.
- [Three-sprint delivery plan](AGILE_DELIVERY_PLAN.md), [Git-backed evidence log](SPRINT1_EVIDENCE_LOG.md) and [slide content](SLIDE_CONTENT.md): the Part 2 planning and integration handoff.
- [Official-template workbook contribution](TeamF4_RAD_Workbook_TaiContribution.xlsx): Tài's partial copy with proposed UC13/UC16 stories/tasks, ownership, Git and AI evidence. All 19 sheets, 141 formulas and three native Burndown charts are preserved. Stand-up, review and Burndown data remain blank. The Team size formula counts only the one populated member row in this partial copy; the team must complete its own roster. The Part 1 workbook in `references/` is preserved as earlier evidence.
- [Final checklist](../../../TAI_FINAL_CHECKLIST.md): requirement-by-requirement PASS, FAIL and NOT VERIFIED evidence.

## UML Rendering Instructions

Install Java and obtain a PlantUML JAR. From the repository root, replace `<plantuml.jar>` with its local path and run the commands below for any source file. PNGs are written beside the `.puml` source.

```text
java -jar <plantuml.jar> -charset UTF-8 -checkonly docs/sprint1/UC13_ManageHubs/diagrams/13-activity.puml
java -jar <plantuml.jar> -charset UTF-8 -tpng docs/sprint1/UC13_ManageHubs/diagrams/13-activity.puml
```

Repeat for the 13 `.puml` files linked above. The final QA used PlantUML `1.2026.10`; sources are editable and the adjacent PNGs were rendered from them.

## Deliverables and Verification Results

Thirteen PlantUML sources have adjacent rendered PNGs. The five new template-driven figures passed syntax checks and visual inspection. UC13/UC16 descriptions, design documents, CRC cards and report links were checked against their diagrams. The new partial workbook retains all 19 official-template sheets, 141 formulas and three Burndown charts; only Tài-owned cells were populated. Exact evidence and remaining issues are in the [final checklist](../../../TAI_FINAL_CHECKLIST.md).

## Known Limitations

- The official [Case Study, Final Project Requirements and report template](https://drive.google.com/drive/folders/14cJnJ9_AhfFeWIxvzuRefNueToF5RyNF) are now available. A team integration DOCX/PDF draft is in `submissions/sprint1/TeamF4_Final_Submission/`; the team has not yet reviewed it or closed the checklist gaps.
- UC13 versus UC14 ownership must be settled by Team F4. Capacity, hub removal, report KPI/period and access policies await a client/lecturer answer.
- UC03/UC04 drafts were copied unchanged from Khang's separate branch for integration. Their Order status names and rejection outcome conflict with Thành's drafts. The current cross-six state consistency check **fails**; a shared status contract remains unverified.
- The Final Project Requirements both demand a working Sprint 2 system/code and say "No coding needed" on page 12. Await lecturer clarification before claiming either interpretation is approved.
- The partial workbook's commit count is a snapshot through `acc5fff`; Git history is authoritative after later commits. Team roster, Sprint Log and submission checklist are incomplete pending team evidence.
