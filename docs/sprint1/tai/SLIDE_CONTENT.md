# Sprint 1 Part 2 — Tài Slide Content for Team PowerPoint

**Author:** Võ Tấn Tài — 524H0126
**Status:** Content draft for insertion into Team F4's shared PowerPoint. The source team `.pptx` has not been provided; no team presentation or review is claimed.

## Slide A — UC13: Manage Hubs and Kitchen Capacity

- **Goal and actor:** Admin maintains hub records and kitchen capacity. The Case Study confirms limited capacity and that busy hubs stop taking new orders.
- **Analysis:** Create/Read/Update/Delete branches, authorization, validation, conflicts and conditional removal. Show [UC13 Activity](../UC13_ManageHubs/diagrams/13-activity.png) and [Hub state machine](../UC13_ManageHubs/diagrams/13-hub-state.png).
- **Design:** Boundary → Controller → Hub/policies → Repository; use [final design class diagram](../UC13_ManageHubs/diagrams/13-final-design-class.png) and [OOD sequence](../UC13_ManageHubs/diagrams/13-ood-sequence.png) if space permits.
- **Open:** Capacity unit/threshold, deletion policy and Part 1 UC14 versus current UC13 ownership.

## Slide B — UC16: Produce Management Reports

- **Goal and actor:** Manager requests sales, hub workload or delivery performance reports; the Case Study confirms these categories.
- **Analysis:** Permission and filters precede read-only retrieval; no-data, incomplete data and failure are distinguished. Show [UC16 Activity](../UC16_ManagementReports/diagrams/16-activity.png).
- **Design:** Definition, read-only source and aggregator produce an explicit result. Show [final design class diagram](../UC16_ManagementReports/diagrams/16-final-design-class.png) or [OOD sequence](../UC16_ManagementReports/diagrams/16-ood-sequence.png).
- **Open:** KPI formulas, period/timezone, scope permissions and data-quality policy under Q5/A-05.

## Slide C — Shared domain and Order lifecycle

- Show the [overall domain model](../shared/domain-model/06-overall-domain.png): Customer types, Order/OrderLine, Hub, Brand, Shipper, Voucher and derived ManagementReport. Mark proposed associations visibly.
- Show the [Order lifecycle](../shared/domain-model/07-overall-order-state.png) only as a draft cross-use-case check. Khang's and Thành's status names and rejection outcome still differ.
- Explain that the UC13 Hub state machine supplies Tài's per-student state-machine evidence in template II 2.2.

## Slide D — Sprint evidence and next decisions

- Use actual Sprint Backlog rows, completed story points and Burndown only after the team workbook is populated from evidence. Git work is listed in [Sprint 1 evidence log](SPRINT1_EVIDENCE_LOG.md).
- Ask the team to settle UC13/UC14 ownership, the shared Order status vocabulary and the UC13 removal policy; ask the lecturer to clarify the Sprint 2 coding contradiction.
- Add real Part 1 feedback applied and a retrospective only after the team documents them.

The official Final Project Requirements call for a **10-minute team presentation** at the Part 2 review, with every member speaking. Team F4 should select the final number of slides and timing; this file does not assign speaking time or invent a review result.
