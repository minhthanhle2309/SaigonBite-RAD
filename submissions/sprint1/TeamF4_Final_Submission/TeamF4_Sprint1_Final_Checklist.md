# Team F4 Sprint 1 Part 2 Verification Checklist

**Prepared by:** Võ Tấn Tài — 524H0126  
**Date:** 16 November 2026  
**Scope:** Sections I–III, six selected use cases, workbook and model source files. PowerPoint is owned by another team member and is not included here. **Overall status: FAIL — team review and mandatory evidence remain outstanding.**

| Requirement | Evidence | Status | Remaining issue |
|---|---|---|---|
| Correct repository and working branch | `feature/tai-uc13-uc16`; `origin` URL matches Team F4 repository | PASS | GitHub access failed during this update; later local commits await push. |
| Official UC IDs and names | Final Project Requirements pp. 2–3; UC03 Place an Order, UC04 Track an Order, UC07, UC10, UC13, UC16 | PASS | The earlier user prompt's UC03/UC04 names differed; official list controls. |
| Six individual owners | Khang 524H0016: UC03/04; Thành 524H0030: UC07/10; Tài 524H0126: UC13/16 | NOT VERIFIED | Part 1 proposal assigned UC14, not UC13, to Tài. Confirm change with team/lecturer. |
| Khang source preserved | `docs/sprint1/UC03_PlaceOrder`, `UC04_TrackOrder`, `shared/khang`; 35 files copied from `origin/feature/khang-uc03-uc04` without changing the source branch | PASS | Khang's own review of integration is pending. |
| Thành source preserved | `docs/sprint1/UC07_ConfirmRejectOrder`, `UC10_DeliverOrder`, `shared/business-process` on Tài's branch | PASS | Thành's own review of integration is pending. |
| Tài source preserved | `docs/sprint1/UC13_ManageHubs`, `UC16_ManagementReports`, `shared/domain-model` | PASS | Client rules remain Proposed / To Confirm. |
| I 1.1 system vision | Report §1.1 | PASS | Part 1 feedback and formal approval record absent. |
| I 1.1 approval record | Report §1.1 explicitly says no record found | FAIL | Add real lecturer feedback and resulting changes. |
| I 1.2 stakeholder chart and Gantt | Report Figures 1–2, Khang's editable `.drawio` sources | PASS | Verify planning dates with the team; no Scrum Master assignment inferred. |
| I 1.3 six-iteration plan, prioritized backlog and risks | Report §1.3 has grouped iteration summary and four risks; workbook has six proposed stories | FAIL | Add the actual six-iteration plan, prioritization and agreed estimates; do not invent them. |
| I 1.4 business narrative and assumption log | Report §§1.4.1–1.4.2 | PASS | Assumptions lack client confirmation. |
| I 1.5–1.6 process and swimlanes | Report Figures 3–5, Thành's `.puml` and PNG | PASS | Order vocabulary still conflicts across branches. |
| I 1.7 functional and measurable nonfunctional requirements | Report §1.7 | FAIL | Only a representative list is integrated; complete and prioritize the team's full requirements and confirm measurable NFR targets. |
| II 2.1 narrative, users, events, actors, ownership, use-case diagram, domain model | Report §§2.1.1–2.1.7; Figures 6–7 | PASS | Ownership and proposed multiplicities require sign-off. |
| II 2.2 fully developed use-case descriptions | Report §§2.2.1–2.2.6 have condensed summaries; six full source descriptions in `docs/sprint1/UC*` | FAIL | Integrate complete numbered main, alternative and exception flows and per-use-case rules into the report; have each author review English wording. |
| II 2.2 Activity and SSD figures for six use cases | Report Figures in §§2.2.1–2.2.6; editable model sources and PNGs | PASS | UC10 has two segments; the report includes the first only. Add/label the second for complete delivery flow. |
| State machine per student | Khang's Order, Thành's Order and Tài's Hub figures; editable sources in `models/` | PASS | The two Order models conflict; both are shown as proposed alternatives. |
| II 2.3 actor CRUD verification | Report §2.3 explicitly identifies gaps | FAIL | Agree persistent class inventory and cover create/read/update/delete or archive for every persistent class. |
| III 3.1–3.6 design class diagrams, sequences and final class diagrams | Six use-case design sections and author-tagged figures | PASS | Some intricate diagrams are small at A4 size; use full-size source images during review. |
| III detailed attributes, methods, visibility and CRC cards | Source design documents contain these; report has class-layer summaries only | FAIL | Bring detailed typed class tables and CRC cards into every report subsection. Thành's CRC cards require a source review. |
| PlantUML syntax | 36 `.puml` files passed PlantUML `-checkonly` on 16 Nov 2026 | PASS | Semantic UML review and peer review still pending. |
| Draw.io source and PNG pairing | 14 `.drawio` files parsed as XML; all have matching readable PNG files | PASS | Some embedded figures shrink in the report; open source/PNG at full size. |
| Cross-six Order status contract | Khang uses `PENDING_CONFIRMATION`, `ACCEPTED`, `READY_FOR_PICKUP`, `DELIVERY_FAILED`; Thành uses `Pending`, `Confirmed`, `Ready`, `Failed`; kitchen rejection outcome differs | FAIL | Team must select a canonical contract, payment transition and reject/cancel distinction. |
| Report template headings and stage scope | Official template retained; Sections IV–V headed Sprint 2 | PASS | Report content gaps above remain. |
| DOCX and PDF file integrity | DOCX opens with 40 embedded figures and 16 tables; 53-page PDF exported by Microsoft Word with 16 top-level bookmarks; all pages rendered to PNG for visual inspection | PASS | Some class/sequence diagrams require full-size viewing; content completeness is not implied. |
| PDF page layout | 53 rendered pages reviewed in contact sheets; no blank page, clipped figure or missing font observed at overview scale | PASS | Fine-print legibility of every figure at printed A4 size is NOT VERIFIED. |
| Updated official workbook template | `TeamF4_SaigonBite_Sprint1_Workbook.xlsx`: 19 sheets, 141 formulas, 3 original charts, ZIP integrity; six use cases and owners populated | PASS | The workbook is an integration copy, not the team's signed/shared master. |
| Product and Sprint Backlogs | Six proposed stories; only Tài's two tasks from prior work | FAIL | Add team-agreed priority, story points, task estimates, remaining hours and peer-review state. |
| Stand-up Log, Review & Retro, Burndown | No verified meetings, review or remaining-hour data supplied; left unfilled | NOT VERIFIED | Team must enter only actual events and measurements. |
| AI Usage Log | Tài row records AI assistance; source files disclose draft status | NOT VERIFIED | Khang and Thành must review their own usage records and retain prompts/outputs as required. |
| Submission Checklist | Workbook Part 2 rows remain Pending | FAIL | Confirm report, PPT, Sprint Log, author IDs, ownership, eLearning and Drive uploads from real evidence. |
| Part 2 PowerPoint | Outside Tài's delegated scope; no PPTX created or included | NOT VERIFIED | Assigned teammate must prepare and verify it. |
| GitHub remote branch matches local | `6dd84e4` and subsequent integration work are local; `origin/feature/tai-uc13-uc16` last verified at `084816a` | FAIL | Retry a normal push only after GitHub access recovers; verify remote hash. Never force push or touch main. |
| Submission readiness | This checklist and handover | FAIL | Resolve report, workbook, ownership, Order contract, peer review, PowerPoint and upload evidence first. |

**Source authority:** `RAD_Sem01_2627_FinalProject_Requirements_SaigonBite.pdf` (03 Nov 2026), SaigonBite Case Study, official Report Template and blank Team Workbook Template. The fictional Team 99 SAMPLE was not used as Team F4 evidence.
