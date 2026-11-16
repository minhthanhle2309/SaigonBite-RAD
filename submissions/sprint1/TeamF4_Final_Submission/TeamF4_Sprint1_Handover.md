# Team F4 Sprint 1 Part 2 Handover

**Prepared by:** Võ Tấn Tài — 524H0126  
**Status:** Integration draft for team review; **not ready for submission**.  
**Repository:** https://github.com/minhthanhle2309/SaigonBite-RAD  
**Working branch:** `feature/tai-uc13-uc16`; unpushed local commits must be preserved.

## Files in this folder

| File | Purpose and how to open | Verification |
|---|---|---|
| `TeamF4_SaigonBite_Sprint1_Report.docx` | Editable official-template report; open in Microsoft Word and update the Table of Contents before final export. | 53-page PDF counterpart exported; content gaps remain in Sections I–III. |
| `TeamF4_SaigonBite_Sprint1_Report.pdf` | Reviewable report with heading bookmarks; open in any PDF reader. | 53 pages, 16 top-level bookmarks, 40 figures; fine-print figure readability requires full-size review. |
| `TeamF4_SaigonBite_Sprint1_Workbook.xlsx` | Official blank 19-sheet workbook populated with verifiable Team F4 ownership and draft backlog. | 141 formulas and 3 native charts retained. Sprint Log evidence is incomplete. |
| `TeamF4_Sprint1_Final_Checklist.md` | Requirement-by-requirement PASS / FAIL / NOT VERIFIED matrix. | Current audit, not a sign-off. |
| `models/` | Editable `.puml` and `.drawio` models plus matching PNGs for six use cases and shared diagrams. | 36 PlantUML files syntax-checked; 14 Draw.io sources parse as XML and have PNG pairs. |

The official Part 2 submission also requires a **PowerPoint** and updated Sprint Log. PowerPoint belongs to another member, is not created here, and must be added by that owner. This package contains no PPTX and no fictional stand-up, review, Burndown or client approval records.

## Model source ownership

- `models/UC03_PlaceOrder` and `models/UC04_TrackOrder`: Mai Bảo Khang — 524H0016, copied from his remote-tracking branch without changing that branch.
- `models/UC07_ConfirmRejectOrder`, `models/UC10_DeliverOrder` and `models/shared/business-process`: Lê Đỗ Minh Thành — 524H0030, already present on Tài's branch.
- `models/UC13_ManageHubs`, `models/UC16_ManagementReports` and `models/shared/domain-model/06-overall-domain.*`, `07-overall-order-state.*`: Võ Tấn Tài — 524H0126.

Open `.drawio` in diagrams.net. Open `.puml` in PlantUML or render with `java -jar plantuml.jar -tpng path/to/file.puml`. Open PNGs directly to inspect small class and sequence labels that are reduced in the PDF. Model source files in `docs/sprint1/` remain authoritative; `models/` is a submission copy.

## Decisions required before submission

1. **Ownership:** The official candidate list defines UC13 as Admin hub CRUD. Team F4's earlier Part 1 proposal assigned UC14 to Tài. Confirm the change and update the approved ownership record.
2. **Order lifecycle:** Khang's customer draft and Thành's kitchen/delivery draft disagree on status names and whether rejection is `CANCELLED` or `Rejected`. Agree the canonical model and update all diagrams, descriptions and the report together.
3. **Client rules:** Confirm hub capacity units/thresholds, deletion or archival policy, reporting KPI formulas, periods and access scope. Keep Proposed / To Confirm until answered.
4. **Report:** Add the complete six-iteration plan, prioritized backlog, full functional/nonfunctional requirements, detailed use-case flows, detailed design tables and CRC cards. Get each author to review the English integration and fix small diagram print size.
5. **Workbook:** Complete priority, estimates, remaining hours and review states from real team planning. Record at least two actual stand-ups per week, real review/retro feedback, Burndown measurements and named Scrum Master only after the events occur.
6. **Submission:** Have the PowerPoint owner add the deck, complete peer review, refresh Word fields/TOC, export the final PDF, verify all files, then submit to eLearning and the shared Drive when authorized.
7. **GitHub:** GitHub DNS/thread failure prevented fetch/push in this session. Verify the local branch against remote and push normally when access recovers. Do not merge, force push or edit `main`.

Sections IV–V are labelled Sprint 2 in the report. The Final Project Requirements both call for a working system and say “No coding needed”; seek lecturer clarification before using either interpretation as an approved plan.
