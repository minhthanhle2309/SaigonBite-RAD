# SaigonBite RAD — Three-Sprint Delivery Plan (Tài Contribution)

**Owner:** Võ Tấn Tài — 524H0126
**Working branch:** `feature/tai-uc13-uc16`
**Basis:** Lecturer's 03 November 2026 update; [Case Study and Final Project Requirements](https://drive.google.com/drive/folders/14cJnJ9_AhfFeWIxvzuRefNueToF5RyNF); [official report template](https://docs.google.com/document/d/1goKSpITT_w0xsNqcBZOmleqeT8h0lEhB/edit); [blank Team Workbook template](https://docs.google.com/spreadsheets/d/1CGLo6JxVCiXPHQeidcYKuvPdM2IsfSVg/edit?gid=326461969). The separate [sample workbook](https://docs.google.com/spreadsheets/d/1VmPGtUHZXGkloQnrvUajiEYWwGVvvBjK/edit?gid=12795987) contains fictional Team 99 data and is not project evidence.

## Delivery stages

| Stage | Published target | Required team submission | Tài's contribution and current position |
|---|---|---|---|
| Sprint 1 / Part 2 | Submit 16 Nov 2026; online review 23 Nov 2026 | Report Sections I–III using the official headings, PowerPoint, updated Sprint Log workbook | UC13/UC16 analysis and design, overall domain model and Order lifecycle have editable diagrams and PNGs. Add UC13 Hub state machine, OOD sequence and final class figures for both use cases; map Tài's report text to the template. Team report, deck and Sprint Log integration remain open. |
| Sprint 2 / Part 3 | Submit and present 30 Nov 2026 | Add Sections IV–V, update deck and Sprint Log, include model sources and Readme | Preserve the Sprint 1 baseline; apply recorded review feedback. Implementation scope needs lecturer clarification because the requirements document conflicts with its own “No coding needed” sentence. Do not claim tests, deployment or a working system without evidence. |
| Sprint 3 / Final | Submit 7 Dec 2026 | Complete report, final deck and Sprint Log, contribution/AI logs, video of about 15 minutes with transcript | Select one of Tài's two use cases for the video after team review. Explain analysis, design and any confirmed programming/UI/testing evidence; apply actual Sprint 1/2 feedback. |

The original six-iteration roadmap remains a planning layer within these three sprints. Team F4 must align its iteration dates and owners in the workbook; this plan does not invent them.

## Sprint 1 template coverage and next integration steps

| Template area | Tài evidence | Status / next step |
|---|---|---|
| I 1.1–1.7 Business Requirements | [Report contribution](../tai-rad-report-contribution.md) describes hub/report context, risks and open assumptions. | Team must supply approval record from actual Part 1 feedback, charts, six-iteration plan, business-process diagrams and ID-based requirements. No lecturer approval is inferred. |
| II 2.1.5 Use cases and owners | [UC13](../UC13_ManageHubs/UC13.md), [UC16](../UC16_ManagementReports/UC16.md). | Official candidate list supports UC13/UC16, but the Part 1 proposal assigned Tài UC14/UC16. Team must resolve the owner table. |
| II 2.1.7 Domain Class Model | [Source and notes](../shared/domain-model/06-overall-model-notes.md). | Confirm proposed cardinalities and reconcile Khang's UC03/04 with Thành's UC07/10 Order vocabulary. |
| II 2.2 per-use-case analysis | UC13/UC16 descriptions, Activity, SSD and UC13 Hub state machine; shared Order state model. | Review lifecycle postconditions and include one state machine attributable to Tài. Exact 2.2 numbering follows team order. |
| II 2.3 CRUD by actor | UC13 design/CRUD table; old workbook Hub row shows a Delete gap. | Team must check every persistent entity across all actors; confirm archive/delete policy. |
| III 3.x detailed design | UC13/UC16 classes, CRC, design diagrams, OOD sequence diagrams and final integrated class diagrams. | Peer review and actual report placement are still needed for Definition of Done. |
| Part 2 PowerPoint | [Slide content draft](SLIDE_CONTENT.md) and 13 PNG figures. | Team source deck is unavailable; integrate Tài's slides into the shared deck and have every member present. |
| Part 2 Sprint Log | [Git evidence log](SPRINT1_EVIDENCE_LOG.md); the [partial workbook](TeamF4_RAD_Workbook_TaiContribution.xlsx) contains Tài's proposed stories/tasks and ownership. The official template has Product Backlog, Sprint Backlog, Stand-up Log, Sprint Review & Retro, Burndown and Submission Checklist. | Team members must complete their roster, estimates, actual stand-ups, hours, feedback and review outcomes in the shared workbook. The partial copy is not a submitted team Sprint Log. |

## Source-backed rules and open decisions

The Case Study confirms that Admin maintains hubs, a hub has limited capacity, a busy hub stops accepting new orders, and Manager reports cover sales, hub workload and delivery performance. It also confirms local/tourist customer types and at most one voucher per order. Capacity units and thresholds, quiet-hub incentive, report KPI formulas, periods and scope access remain open. The official candidate list supports UC13, but team ownership conflicts with the Part 1 proposal's UC14 assignment.

The Final Project Requirements demand a working system, SQL/code, deployment and a tagged release in Sprint 2 (pages 4 and 6–7), but also state “No coding needed” (page 12). The lecturer's newer announcement describes this as an Agile Modelling Project without mandatory application programming. Team F4 should record a lecturer clarification before committing to an implementation interpretation. Sprint 1 analysis and modelling proceed independently of that decision.

## Agile evidence rules

- Name one Scrum Master per sprint when the team actually assigns the role; rotate it as the requirements specify. No assignment is inferred here.
- Hold at least two stand-ups per week and record one row per attendee only after each meeting. Git commits are work evidence, not proof that a stand-up happened.
- Record Sprint Review, retrospective, lecturer feedback and Burndown remaining hours only from real events and measured task data. The sample workbook's Team 99 entries must never be copied as Team F4 facts.
- The Definition of Done includes teammate review, author ID, consistency and report inclusion. A rendered diagram alone is an authored artifact, not a completed team submission.
- Each student needs **more than 10 meaningful commits over the project**. Tài had 13 actual commits through `084816a` after the UC13, UC16 and domain reconciliation packages. Count only distinct, substantive work and verify authorship/remote history; do not create empty or cosmetic commits.
- Commit and push Tài's changes only on `feature/tai-uc13-uc16`. Do not merge/push `main`, force push or create a Pull Request.

## Planned work packages

1. **Official-source reconciliation — completed as draft artifacts:** UC13, UC16 and shared models were corrected against the Case Study and requirements. Missing state, OOD sequence and final class figures were added; PlantUML/PNG QA passed. Three focused commits were pushed and remotely verified.
2. **Sprint 1 integration contribution — prepared for team:** Map text and 13 figures to the exact report template subsections; prepare slide content and a Git-backed evidence log. Team report/deck integration and peer review remain open.
3. **Team workbook transfer — Tài copy prepared:** The official blank workbook was used, not the fictional sample. Only Tài-owned proposed backlog/task/contribution entries were added; meeting, review and Burndown fields remain blank. The old Part 1 workbook is preserved as historical evidence. Team F4 must transfer/reconcile these rows into its shared working copy.
4. **Team review and submission:** Resolve UC13/UC14 ownership, cross-branch Order statuses, CRUD gaps, proposed rules and peer review. Team members integrate the report, deck and workbook; only then can the submission checklist be marked complete.
