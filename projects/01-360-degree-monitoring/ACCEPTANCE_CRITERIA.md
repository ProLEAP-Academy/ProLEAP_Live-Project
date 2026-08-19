# 360-Degree Monitoring - Acceptance Criteria

| ID | Acceptance criterion | Evidence |
|---|---|---|
| AC-MON-001 | Host CPU, memory and filesystem metrics are visible for at least 60 minutes of test activity. | Dashboard/query evidence |
| AC-MON-002 | An HTTP/service probe correctly distinguishes healthy and unavailable states. | Probe metric + test output |
| AC-MON-003 | Application or system logs can be searched centrally by time and workload/host. | Log query evidence |
| AC-MON-004 | A service-outage alert fires within the project-defined detection window. | Alert timeline |
| AC-MON-005 | Recovery resolves the alert automatically after the configured condition clears. | Alert resolution evidence |
| AC-MON-006 | A resource-pressure scenario appears on the dashboard and triggers the intended alert when threshold/duration is met. | Dashboard + alert evidence |
| AC-MON-007 | Critical alert text includes owner/action/runbook reference. | Alert rule/output |
| AC-MON-008 | Monitoring stack can be recreated from repository instructions/configuration. | Clean redeploy demonstration |
| AC-MON-009 | No real secret exists in version-controlled files. | Secret scan/review |
| AC-MON-010 | Team diagnoses at least one seeded incident from telemetry before being told the injected fault. | Live demo |
| AC-MON-011 | A trace for a sample request is visible in the tracing backend and can be correlated with the logs/metrics for the same request or time window. | Trace query + correlated log/metric evidence |
