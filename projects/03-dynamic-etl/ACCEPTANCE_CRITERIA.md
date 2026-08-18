# Dynamic ETL - Acceptance Criteria

| ID | Acceptance criterion | Evidence |
|---|---|---|
| AC-DETL-001 | Valid ZIP is ingested over approved encrypted transport and assigned a run ID/checksum. | Run manifest/log |
| AC-DETL-002 | Multiple workbooks in one ZIP are processed without fixed file-count assumptions. | Fixture test |
| AC-DETL-003 | Multiple Empirical/Regression types in one workbook produce separate correlated output records. | Exact expected-output test |
| AC-DETL-004 | No-type model sheets produce `Type = NULL`. | Fixture test |
| AC-DETL-005 | Output workbook contains all required legacy columns in approved order. | Schema assertion |
| AC-DETL-006 | Canonical output uses `model_YYYYMMDD.xlsx`. | File evidence |
| AC-DETL-007 | Model data is persisted to logical `AnalystData` target with run lineage. | DB query |
| AC-DETL-008 | Latest Datasheet month is persisted with all 14 legacy fields. | DB query |
| AC-DETL-009 | Same-day rerun replaces/updates prior logical data without duplicate published records. | Rerun integration test |
| AC-DETL-010 | Successful run archives original ZIP and cleans temporary extraction files. | Filesystem/object-store evidence |
| AC-DETL-011 | Invalid workbook/ZIP enters quarantine and does not publish canonical output. | Negative test |
| AC-DETL-012 | Database failure does not leave a run marked successful or a partially accepted data set. | Failure injection |
| AC-DETL-013 | A normal agreed-size batch completes end to end in <=30 minutes. | Timed test |
| AC-DETL-014 | Pipeline automatically runs unit and representative workbook tests before deployment. | CI evidence |
| AC-DETL-015 | No production secrets are committed; runtime secrets are externalized. | Secret scan/config review |
| AC-DETL-016 | Operator can identify failed run, failure stage and corrective action from logs/metrics/runbook. | Controlled demo |
