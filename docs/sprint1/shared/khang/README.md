# KHANG Sprint 1 handoff

Responsible student: Mai Bảo Khang — 524H0016. AI-assisted draft; assumptions and integration decisions require team/client review. Author email for this contribution: langkang2707@gmail.com.

## Files

- [UC03 description](../../UC03_PlaceOrder/UC03.md) and [design / CRC / Order lifecycle](../../UC03_PlaceOrder/Design.md).
- [UC04 description](../../UC04_TrackOrder/UC04.md) and [design / CRC](../../UC04_TrackOrder/Design.md).
- [Section I](Section_I.md): business requirements, planning, backlog, risks and assumptions. This Markdown retains the detailed reference text; the report below is the concise hand-in contribution.
- [25-page Word report](../../../../submissions/sprint1/KHANG_524H0016_Report.docx): current report for KHANG, including the AI Usage Log appendix. Page count verified in Microsoft Word at A4 using Segoe UI; other viewers may paginate differently.
- Each diagram has an editable `.drawio` and a matching `.png`. The UC03 folder includes Khang's Order State Machine. This folder contains stakeholder chart, Gantt and the six-main-UC portfolio diagram.

The Word report covers Khang's Sections I–III contribution. It does not replace the full team BRS/SRS, the official Canvas template or Sections IV–V. Sprint 1 does not include application source code. No client approval, executed application tests or deployment is claimed.

## Integration decisions before merging

The main branch already contains Thành's fulfilment models. Khang's diagrams are proposed models and must be reconciled with them; the two vocabularies are **not yet a single agreed contract**.

| Khang vocabulary | Existing Thành vocabulary | Required decision |
|---|---|---|
| PENDING_CONFIRMATION | Pending | Confirm common name and admission condition, including payment eligibility. |
| ACCEPTED | Confirmed | Confirm equivalent business transition and common name. |
| PREPARING / READY_FOR_PICKUP | Preparing / Ready | Confirm names and the owner of UC08 preparation/ready support. |
| OUT_FOR_DELIVERY / DELIVERED / DELIVERY_FAILED | OutForDelivery / Delivered / Failed | Confirm names, delivery reason and COD fields. |
| CANCELLED for kitchen rejection, cancellation or unpaid expiry | Rejected and Cancelled are distinct states | Decide whether to preserve distinct states or use a reason code; no automatic one-to-one mapping. |
| AWAITING_PAYMENT before kitchen admission | No corresponding state in the current shared state diagram | Allocate payment/timeout support and decide the shared lifecycle before implementation. |

- Assumption IDs in the separate drafts are local references. For example A02 and A04 have different meanings in Thành's UC documents and Khang's log. Agree one team-wide Assumption Log and update references before assembling the report.
- Khang's `TEAM_UseCases` represents the selected **six main UCs**. The existing shared `03-use-cases.puml` represents a broader fulfilment context. Decide how to present both scopes in the final report.
- Tài must verify persistent-entity CRUD/archive coverage. Do not mark CRUD complete while Order/archive or master-data ownership remains unresolved.
- Business Process, Swimlane and Events Table remain Thành's responsibility; the overall Domain Model and CRUD verification remain Tài's. The branch adds Khang's artifacts for review without replacing those shared models.

## Commit grouping

1. UC03 analysis, design, CRC, state machine and diagram source/exports.
2. UC04 analysis, design, CRC and diagram source/exports.
3. Section I, portfolio/planning charts, this integration note and the concise Word report.

Keep the AI labels and update the AI Usage Log with the student's actual review and edits. The source requirements and internal assignment remain the authority for submission rules.
