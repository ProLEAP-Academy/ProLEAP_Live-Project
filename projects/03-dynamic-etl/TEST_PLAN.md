# Dynamic ETL - Test Plan

## 1. Unit tests

Test pure logic independently:

- filename -> ticker parsing;
- sheet-name -> type parsing;
- date/quarter/year parsing;
- model-pair correlation;
- numeric conversion;
- output record construction;
- Datasheet latest-month selection;
- business-key/idempotency logic;
- error classification.

## 2. Workbook fixture tests

Maintain sanitized synthetic fixtures for:

1. one workbook, one type;
2. one workbook, no explicit type;
3. one workbook, multiple model types;
4. multiple workbooks in one ZIP;
5. missing Regression pair;
6. missing Empirical pair;
7. malformed numeric value;
8. moved but still label-identifiable fields;
9. unsupported schema/version;
10. Datasheet with multiple months.

Assert exact expected rows, not only "script exits 0".

## 3. Integration tests

- inbound archive -> extraction;
- ETL -> output workbook;
- ETL -> test database transaction;
- archive/cleanup behavior;
- quarantine behavior;
- same-day rerun replacement;
- interrupted run recovery.

## 4. Failure tests

- corrupted ZIP;
- password-protected/unreadable workbook if unsupported;
- database unavailable;
- insufficient output disk/storage;
- permission denied;
- duplicate source upload;
- process terminated mid-run.

The expected terminal state and retry procedure must be documented for each.

## 5. Performance test

Define an agreed reference batch size before testing, for example:

- number of ZIPs: 1;
- workbooks: N;
- max workbook size: X MB;
- total input size: Y MB;
- total supported model sheets: Z.

Then measure stage durations and total runtime. The project-wide acceptance target remains <=30 minutes for the agreed normal workload.

## 6. Data reconciliation

For at least one fixture, manually calculate/verify expected source values and compare:

- workbook output;
- database model table;
- Datasheet table;
- record counts;
- source lineage.

## 7. Security tests

- secret scan repository;
- verify SFTP/HTTPS instead of plaintext FTP in the reference deployment;
- verify least-privilege file permissions;
- verify sensitive values are not printed in logs;
- verify archive/quarantine permissions.
