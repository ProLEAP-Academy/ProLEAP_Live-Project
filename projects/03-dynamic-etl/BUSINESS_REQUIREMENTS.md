# Dynamic ETL Automation Platform - Business Requirements

## 1. Business need

The business receives ZIP packages containing multiple client Excel workbooks. Each workbook can contain Empirical Model sheets, Regression Model sheets and a Datasheet. Quarterly model values must be consolidated into a standardized output workbook and persisted into relational databases.

The process must be automated, secure, repeatable and operationally supportable.

## 2. Goals

- automate the complete ingest -> extract -> transform -> validate -> publish -> archive flow;
- preserve integrity and atomicity of output/database writes;
- support any reasonable number of source files/supported sheets within a batch;
- complete a normal batch in <=30 minutes;
- support safe same-day reruns;
- retain traceability from source package to output rows;
- expose failures with actionable diagnostics;
- deploy through CI/CD and repeatable infrastructure/configuration.

## 3. Scope

### In scope

- secure file ingestion;
- ZIP validation/extraction;
- Excel parsing;
- Empirical/Regression correlation by type;
- output Excel generation;
- relational persistence;
- Datasheet persistence;
- archive/quarantine/cleanup;
- scheduling/event triggering;
- CI/CD;
- operational telemetry;
- troubleshooting/runbook.

### Out of scope by default

- redesigning the business calculation formulas inside the source workbooks;
- editing source workbooks;
- human identity/access-management platform beyond project needs;
- graphical ETL designer;
- production customer data in the public training repository.

## 4. Secure ingestion requirements

| ID | Requirement | Priority | Legacy mapping |
|---|---|---|---|
| DETL-ING-001 | Provide an automated, documented ingestion endpoint/location on an approved cloud or lab platform. | Must | BR1 |
| DETL-ING-002 | Use encrypted transport such as SFTP/SSH or object-storage HTTPS. Plain FTP is legacy compatibility only and is not the reference design. | Must | BR1 modernized |
| DETL-ING-003 | Protect persistent source/output storage with encryption at rest where the platform supports it; a Linux block-device implementation may use encrypted volume/LUKS. | Must | BR2 |
| DETL-ING-004 | Validate file type, ZIP readability, size limits and expected contents before processing. | Must | Gap filled |
| DETL-ING-005 | Generate a SHA-256 checksum and run manifest for each accepted source archive. | Must | Gap filled |
| DETL-ING-006 | Process each run in an isolated working directory. | Must | BR3/BR6 clarified |
| DETL-ING-007 | Move invalid/unprocessable inputs to quarantine with a machine-readable failure reason. | Must | Gap filled |

## 5. Orchestration requirements

| ID | Requirement | Priority | Legacy mapping |
|---|---|---|---|
| DETL-ORCH-001 | Support scheduled execution using a systemd timer/cron or equivalent cloud scheduler. | Must | BR3 |
| DETL-ORCH-002 | Trigger an orchestration entrypoint that validates the batch, extracts the ZIP and invokes the Python ETL process. | Must | BR3 |
| DETL-ORCH-003 | Assign every execution a unique `run_id`. | Must | Gap filled |
| DETL-ORCH-004 | Prevent the same source archive from being processed concurrently unless explicitly configured. | Must | Gap filled |
| DETL-ORCH-005 | Use explicit terminal states such as `completed`, `failed`, `quarantined` and `partial` if partial mode is allowed. | Must | Gap filled |

## 6. Transformation requirements

| ID | Requirement | Priority | Legacy mapping |
|---|---|---|---|
| DETL-TR-001 | Extract Excel files from the accepted ZIP into the run working directory. | Must | BR3 |
| DETL-TR-002 | Detect all supported Empirical Model and Regression Model sheets in each workbook. | Must | BR9-BR12 |
| DETL-TR-003 | Determine the `Type` represented by each model sheet from the sheet naming/business rule. | Must | BR11, BR15-BR17 |
| DETL-TR-004 | When no type is present, store `Type` as NULL. | Must | BR17 |
| DETL-TR-005 | Correlate Empirical and Regression data for the same type into one output record. | Must | BR26 |
| DETL-TR-006 | Extract `Quarter` and `Year` from the Regression Model according to the validated workbook schema. | Must | BR18-BR19 |
| DETL-TR-007 | Extract Estimated Total Sold, Estimated Sold Max and Estimated Sold Min from the Empirical Model. | Must | BR9, BR20-BR22 |
| DETL-TR-008 | Extract Forecast w/o SA Actual, Forecast w/o SA Max and Forecast w/o SA Min from the Regression Model. | Must | BR10, BR23-BR25 |
| DETL-TR-009 | Derive `Ticker`/company code from the source filename using a documented parsing rule. | Must | BR13 |
| DETL-TR-010 | Emit a separate output record for each source workbook + type combination. | Must | BR14-BR15 |
| DETL-TR-011 | Parse the Datasheet and extract the latest month's records into the defined Data dataset. | Must | BR29 |
| DETL-TR-012 | Prefer semantic labels/anchors in the workbook over naked hard-coded coordinates; if cell coordinates are required, centralize them in versioned schema configuration. | Must | BR18-BR25 clarified |
| DETL-TR-013 | Detect unsupported/missing/duplicated model pairs and fail or quarantine according to a documented rule rather than silently producing incomplete data. | Must | Gap filled |

## 7. Output workbook requirements

| ID | Requirement | Priority | Legacy mapping |
|---|---|---|---|
| DETL-OUT-001 | Write the consolidated output under the configured data-output location. | Must | BR4 |
| DETL-OUT-002 | Preserve the canonical filename `model_YYYYMMDD.xlsx` for the current run date. | Must | BR5 |
| DETL-OUT-003 | Resolve the legacy same-day filename collision by writing atomically and storing each historical run under a unique run-ID/timestamp archive path. | Must | BR8 + BR28 clarified |
| DETL-OUT-004 | Output columns must match the approved data dictionary and ordering. | Must | BR13 |
| DETL-OUT-005 | Do not publish the final canonical workbook until all mandatory validations pass. | Must | Reliability NFR clarified |

## 8. Database requirements

| ID | Requirement | Priority | Legacy mapping |
|---|---|---|---|
| DETL-DB-001 | Persist consolidated model output to a relational dataset logically named `AnalystData`. | Must | BR27 |
| DETL-DB-002 | Persist latest Datasheet records to a relational dataset logically named `Data`. | Must | BR29 |
| DETL-DB-003 | Same-day rerun behavior must be idempotent: previously published data for the applicable logical run date/source scope must be replaced transactionally, not duplicated. | Must | BR28 |
| DETL-DB-004 | Use transactions so a failed database write does not leave an accepted run partially committed. | Must | Reliability NFR |
| DETL-DB-005 | Store run lineage (`run_id`, source archive checksum/name, processed timestamp) with persisted data or through linked metadata. | Must | Gap filled |
| DETL-DB-006 | Apply database schema changes through version-controlled migrations. | Should | Gap filled |

## 9. Archive and cleanup requirements

| ID | Requirement | Priority | Legacy mapping |
|---|---|---|---|
| DETL-ARC-001 | Remove extracted temporary files after a successful terminal workflow. | Must | BR6 |
| DETL-ARC-002 | Archive/move the original ZIP after successful processing. | Must | BR7 |
| DETL-ARC-003 | Retain failed source packages in quarantine or failed-run archive long enough for diagnosis. | Must | Gap filled |
| DETL-ARC-004 | Never delete the only copy of a source package before publication and database commit succeed. | Must | Reliability clarified |
| DETL-ARC-005 | Retention periods for source archives, outputs, logs and quarantine must be configurable/documented. | Should | Gap filled |

## 10. Exact output model fields

The legacy output schema is preserved:

1. Date
2. Ticker
3. Type
4. Quarter
5. Year
6. Estimated Total Sold
7. Estimated Sold Max
8. Estimated Sold Min
9. Forecast w/o SA Actual
10. Forecast w/o SA Max
11. Forecast w/o SA Min

See [`DATA_DICTIONARY.md`](DATA_DICTIONARY.md).

## 11. Datasheet fields

The legacy Datasheet target schema is preserved:

`Date, FacilityType, BedSize, Region, Manufacturer, Ticker, Group, Therapy, Anatomy, SubAnatomy, ProductCategory, Quantity, AvgPrice, TotalSpend`

## 12. Non-functional requirements

| ID | Area | Requirement |
|---|---|---|
| DETL-NFR-001 | Reliability | A run must either publish a valid committed result or end in a diagnosable failed/quarantined state; no silent partial success. |
| DETL-NFR-002 | Data integrity | Output/database data must remain consistent with validated source records and same-day rerun policy. |
| DETL-NFR-003 | Robustness | Handle multiple workbooks and multiple model-sheet types without fixed file-count assumptions. |
| DETL-NFR-004 | Performance | Normal end-to-end batch must complete in <=30 minutes in the agreed test environment and dataset size. |
| DETL-NFR-005 | Scalability | Processing design should avoid loading all source workbooks into memory simultaneously when not necessary. |
| DETL-NFR-006 | Security | Encrypt transport, protect secrets, restrict file/database access and avoid logging sensitive workbook contents unnecessarily. |
| DETL-NFR-007 | Observability | Emit run status, duration, files processed, records produced, records rejected, validation failures and terminal error information. |
| DETL-NFR-008 | Maintainability | Workbook schema/anchor rules and business mappings must be centralized and testable. |
| DETL-NFR-009 | Portability | Business logic should not depend on one cloud provider's proprietary runtime unless explicitly approved. |
| DETL-NFR-010 | Recoverability | Operator must be able to rerun a failed batch safely after correcting the underlying issue. |

## 13. CI/CD requirements

- all application, configuration and infrastructure code is version controlled;
- lint/unit tests run automatically;
- representative workbook fixture tests run automatically;
- dependency/secret/security checks appropriate to the implementation run in CI;
- deployable artifact is versioned;
- deployment uses repeatable automation;
- environment secrets are injected at deployment/runtime, not embedded in source.

## 14. Legacy ambiguity resolutions

### BR20-BR22 and BR23-BR25 cell references

The legacy document states that three Empirical values are in column F and three Regression values are in column R, but does not uniquely identify rows/labels. The modern requirement therefore **does not invent row numbers**. The implementation must validate the real workbook format and map values by stable labels/anchors or centralized schema configuration.

### BR5 and BR8 same-day filename conflict

The legacy specification requires `model_YYYYMMDD` while also saying every execution creates a new file. Those statements conflict on same-day reruns. The modern rule preserves the canonical business filename while storing run-specific historical artifacts by timestamp/run ID.

### FTP/CentOS dependency

The original business outcome was automated cloud file ingestion, not insecure transport as a business goal. Secure SFTP/object-storage transport supersedes plain FTP for the reference implementation. A legacy FTP adapter may be built only as an isolated compatibility component if a trainer explicitly requires it.

## 15. Complete legacy BR1-BR29 traceability

| Legacy ID | Original intent | Modern requirement(s) |
|---|---|---|
| BR1 | Automate CentOS FTP server on cloud | DETL-ING-001, DETL-ING-002; runtime/transport modernized |
| BR2 | Encrypt `/opt` storage | DETL-ING-003 |
| BR3 | Cron -> Linux script -> unzip -> Python | DETL-ORCH-001, DETL-ORCH-002, DETL-TR-001 |
| BR4 | Create output Excel in `/opt/dataout` | DETL-OUT-001 |
| BR5 | `model_YYYYMMDD` filename | DETL-OUT-002 |
| BR6 | Delete extracted Excel after processing | DETL-ARC-001 |
| BR7 | Archive/move ZIP to output area | DETL-ARC-002 |
| BR8 | New output per execution | DETL-OUT-003 |
| BR9 | Read Estimated Total/Min/Max sold | DETL-TR-007 |
| BR10 | Read Forecast Actual/Min/Max | DETL-TR-008 |
| BR11 | Multiple model sheets with type | DETL-TR-002, DETL-TR-003 |
| BR12 | Read every supported model screen/sheet | DETL-TR-002 |
| BR13 | Required output columns | DETL-OUT-004 + Data Dictionary |
| BR14 | Source data becomes output records | DETL-TR-010 |
| BR15 | Multiple types produce separate records | DETL-TR-010 |
| BR16 | Type from model sheet name | DETL-TR-003 |
| BR17 | Missing type -> NULL | DETL-TR-004 |
| BR18 | Quarter from Regression Model | DETL-TR-006 |
| BR19 | Year from Regression Model | DETL-TR-006 |
| BR20 | Estimated Total Sold | DETL-TR-007 |
| BR21 | Estimated Max Sold | DETL-TR-007 |
| BR22 | Estimated Min Sold | DETL-TR-007 |
| BR23 | Forecast w/o SA Actual | DETL-TR-008 |
| BR24 | Forecast w/o SA Max | DETL-TR-008 |
| BR25 | Forecast w/o SA Min | DETL-TR-008 |
| BR26 | Empirical + Regression same type in one record | DETL-TR-005 |
| BR27 | Persist output in MySQL `AnalystData` | DETL-DB-001 |
| BR28 | Same-day rerun replaces earlier data | DETL-DB-003 |
| BR29 | Latest Datasheet month persisted to `Data` with specified columns | DETL-TR-011, DETL-DB-002 |
