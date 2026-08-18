# GitHub Contributor Intelligence - Acceptance Criteria

| ID | Acceptance criterion | Evidence |
|---|---|---|
| AC-GCI-001 | Authenticated client can create an analysis job and receives `202` plus job ID. | API test |
| AC-GCI-002 | Invalid repository/date input is rejected with stable error format. | Negative API tests |
| AC-GCI-003 | `all` branch mode enumerates repository branches through GitHub API. | Logs/test fixture |
| AC-GCI-004 | A commit reachable from two branches is counted once by SHA. | Deterministic fixture test |
| AC-GCI-005 | Pagination is exercised with a fixture/repository requiring more than one API page. | Integration test |
| AC-GCI-006 | Privacy/noreply email is not classified as an employer/company domain. | Unit/integration test |
| AC-GCI-007 | Completed analysis persists repository, period, run timestamp and aggregated domain statistics. | DB query |
| AC-GCI-008 | Retried POST with same idempotency key does not create an unintended duplicate job. | API test |
| AC-GCI-009 | Simulated GitHub rate-limit response produces backoff/retry or controlled partial/failure behavior rather than a tight loop. | Failure test |
| AC-GCI-010 | GitHub/database credentials are not present in Git or logs. | Secret scan/log review |
| AC-GCI-011 | Worker failure leaves a queryable terminal job state with sanitized error information. | Failure test |
| AC-GCI-012 | Reference environment can be deployed from documented IaC/automation. | Clean deployment evidence |
| AC-GCI-013 | Test harness demonstrates create -> poll -> summary flow. | Demo |
| AC-GCI-014 | Running a new analysis for a repository/date range already analyzed produces a new job record without altering or corrupting the results of the earlier job. | DB query comparing both job results |
