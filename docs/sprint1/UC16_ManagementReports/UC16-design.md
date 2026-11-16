# UC16 — Design Classes, CRC Cards, and Report Logic Review

**Author:** Võ Tấn Tài — 524H0126

**Status:** Proposed design aligned with [UC16 specification](UC16.md). KPI, period, access and data-quality decisions remain **To Confirm** under workbook Q5/A-05.

## Design classes

| Layer | Class | Attributes (`-` private) | Operations (`+` public) | Responsibility |
|---|---|---|---|---|
| Boundary/View | `ManagementReportView` | `-selectedType: ReportType?`, `-selectedPeriod: Period?`, `-selectedScope: Scope?` | `+showPermittedOptions(options)`, `+collectRequest()`, `+showReport(report)`, `+showNoData(filters)`, `+showError(message)` | Collects request and presents result/status; performs no aggregation. |
| Controller | `ManagementReportController` | `-accessPolicy: ReportAccessPolicy`, `-catalog: ReportDefinitionCatalog`, `-source: ReportSourceRepository`, `-aggregator: ReportAggregator` | `+listAvailableReports(actor)`, `+produceReport(actor, request)` | Validates scope, obtains definition and eligible source data, coordinates aggregation and maps errors. |
| Domain policy | `ReportAccessPolicy` | `-permissionRules: PermissionRules` | `+permittedOptions(actor)`, `+canRead(actor, reportType, scope)` | Decides which reports and data scopes the actor may access. Exact rules **To Confirm**. |
| Domain | `ReportDefinition` | `-type: ReportType`, `-metricRules: MetricRules`, `-eligibilityRules: EligibilityRules`, `-qualityRules: QualityRules` | `+validateRequest(request)`, `+eligible(record)`, `+evaluateQuality(records)` | Holds a confirmed report's calculation and source inclusion rules. These definitions are **To Confirm**. |
| Domain service | `ReportAggregator` | `-definition: ReportDefinition` | `+aggregate(records, request): ManagementReport`, `+emptyResult(request): NoDataResult` | Computes values using the selected definition and separates no-data from numeric zero. |
| Domain result | `ManagementReport` | `-type: ReportType`, `-period: Period`, `-scope: Scope`, `-values: ReportValues`, `-dataStatus: DataStatus`, `-asOf: Timestamp?` | `+summary()`, `+isComplete()` | Immutable report result with context and completeness metadata. Snapshot/as-of semantics **To Confirm**. |
| Data Access | `ReportDefinitionCatalog` | `-definitions: DefinitionStore` | `+listAvailable()`, `+find(type)` | Provides approved definitions; must not substitute guessed formulas for missing definitions. |
| Data Access | `ReportSourceRepository` | `-dataSource: DataSource` | `+readEligible(request, definition)`, `+readStatus(request)` | Read-only access to permitted source records and source-quality status. Exact data mapping **To Confirm**. |

`ReportType`, `Period`, `Scope`, `MetricRules`, `EligibilityRules`, `QualityRules`, `ReportValues` and `DataStatus` are conceptual types. Their enumerations and fields must be fixed from the Case Study or client response. `asOf` is proposed metadata for concurrent data changes, not an approved rule.

### Collaboration and error mapping

1. `ManagementReportView` submits `listAvailableReports()` or `produceReport(reportType, period, scope)` to the controller.
2. The controller asks `ReportAccessPolicy` for the actor's allowed report and scope **before** retrieving source data.
3. The controller retrieves a `ReportDefinition`; an absent or unapproved definition produces an unsupported-report result, not a guessed calculation.
4. The definition validates period/scope, and `ReportSourceRepository` reads eligible data without modifying `Order`, `Hub`, delivery or payment records.
5. No records produce `NoDataResult`. Retrieval failure produces `ReportUnavailable`. Incomplete source data is marked or rejected according to a confirmed `QualityRules` decision. A complete set is aggregated into `ManagementReport`.
6. The view displays type, period, scope and data status so a Manager can distinguish a valid result, an empty result and an unavailable result.

## CRC cards

| Class | Responsibilities | Collaborators |
|---|---|---|
| `ManagementReportView` | Capture request; display permitted choices, report, no-data or error. | `ManagementReportController` |
| `ManagementReportController` | Coordinate authorization, definition lookup, source retrieval, aggregation and error mapping. | `ManagementReportView`, `ReportAccessPolicy`, `ReportDefinitionCatalog`, `ReportSourceRepository`, `ReportAggregator` |
| `ReportAccessPolicy` | Enforce type and scope permissions. | `ManagementReportController` |
| `ReportDefinition` | Validate filters; define eligible source records, KPI formula and quality requirement once approved. | `ReportDefinitionCatalog`, `ReportAggregator`, `ReportSourceRepository` |
| `ReportAggregator` | Compute defined values; preserve no-data semantics. | `ReportDefinition`, `ManagementReport` |
| `ManagementReport` | Hold immutable values and context; expose completeness. | `ReportAggregator`, `ManagementReportView` |
| `ReportDefinitionCatalog` | Return only approved report definitions. | `ManagementReportController`, `ReportDefinition` |
| `ReportSourceRepository` | Read permitted source records and data status; never write source records. | `ManagementReportController`, `ReportDefinition` |

## Access, aggregation and exception verification

| Check | Expected behaviour | Open decision |
|---|---|---|
| Unauthorized actor/type/scope | Reject before source query; reveal no protected values. | Exact role and row-level permission matrix. |
| Invalid period or scope | Reject and request correction. | Supported periods, timezone, scope dimensions. |
| Missing definition | Return unsupported/unavailable; do not invent KPI values. | Official metric formulas and record inclusion criteria. |
| No eligible records | Return explicit no-data result; do not imply a valid numeric zero. | Whether empty exports are allowed. |
| Incomplete or inconsistent records | Show incomplete/unavailable status under the approved quality rule. | Completeness thresholds and treatment of late updates. |
| Retrieval or aggregation failure | Report failure; do not show partial values as complete. | Retry, timeout and snapshot policy. |
| Concurrent changes | Identify the data snapshot or disclose uncertainty. | As-of and consistency model. |
| Successful report | Display values with type, period, scope and data status; no operational mutation. | Source tables, KPI units and display format. |

The existing shared domain model already contains `Order`, `Hub` and `Shipper` for UC07/UC10. UC16's read model should integrate with the eventual overall domain model without editing those team-owned diagrams in this phase. Export, report scheduling and stored report history are not included until confirmed.
