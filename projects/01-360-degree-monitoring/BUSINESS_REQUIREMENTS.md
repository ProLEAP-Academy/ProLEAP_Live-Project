# 360-Degree Monitoring Platform - Business Requirements

## 1. Business need

Operations teams require a single, repeatable way to detect service degradation, understand probable cause and act before or during an outage. The solution must correlate host health, endpoint availability, application telemetry and logs sufficiently for a learner/operator to diagnose a controlled failure.

## 2. Goals

- reduce blind spots in host/application health;
- detect actionable failures quickly;
- centralize evidence used for diagnosis;
- make dashboards/alerts reproducible as code/configuration;
- provide documented recovery actions;
- demonstrate open-source observability principles.

## 3. Scope

### In scope
- Linux host metrics;
- application or web endpoint availability;
- centralized logs;
- dashboards;
- alert rules and notification routing;
- deployment automation;
- runbooks;
- controlled failure/recovery test.

### Out of scope by default
- enterprise multi-region HA;
- petabyte-scale log retention;
- paid SaaS monitoring dependency;
- production PII/customer data.

## 4. Functional requirements

| ID | Requirement | Priority |
|---|---|---|
| MON-FR-001 | Collect CPU, memory, filesystem and basic network/system metrics from at least one Linux host. | Must |
| MON-FR-002 | Monitor at least one service/HTTP endpoint using an availability probe. | Must |
| MON-FR-003 | Centralize logs from the monitored workload or host. | Must |
| MON-FR-004 | Provide at least one host dashboard and one service dashboard. | Must |
| MON-FR-005 | Create alerts for at least three operational symptoms, including service unavailable and resource pressure. | Must |
| MON-FR-006 | Route alerts to a configured notification target suitable for the training environment. | Must |
| MON-FR-007 | Attach a runbook reference or operator instruction to critical alerts. | Must |
| MON-FR-008 | Preserve dashboards and alert rules in version-controlled configuration where the chosen tooling supports it. | Must |
| MON-FR-009 | Expose health status for the monitoring components themselves. | Must |
| MON-FR-010 | Demonstrate a controlled failure and recovery while telemetry captures the incident. | Must |
| MON-FR-011 | Record deployment/release annotations or equivalent change context on dashboards. | Should |
| MON-FR-012 | Collect application traces through OpenTelemetry and store them in a tracing backend (for example Grafana Tempo or Jaeger), correlated with logs and metrics for the same request/service. | Should |
| MON-FR-013 | Provide service-level indicators such as availability, latency or error rate. | Should |
| MON-FR-014 | Support more than one monitored host through repeatable configuration. | Should |

Traces are what make this genuinely "360-degree": metrics tell you something is wrong, logs and traces tell you where and why. A project that only implements metrics and logs has covered two of the three observability pillars and should say so explicitly rather than claim full coverage.

## 5. Non-functional requirements

| ID | Area | Requirement |
|---|---|---|
| MON-NFR-001 | Security | Monitoring endpoints and dashboards must not expose credentials; administrative access must be protected. |
| MON-NFR-002 | Repeatability | Deployment must be reproducible using documented automation such as Docker Compose, Ansible, Terraform or Kubernetes manifests. |
| MON-NFR-003 | Reliability | Restarting monitoring components must not require manual recreation of dashboards/rules. |
| MON-NFR-004 | Operability | A new operator must be able to identify the source of a seeded incident using the documented dashboards/logs/runbook. |
| MON-NFR-005 | Alert quality | Alerts must be actionable and avoid duplicate/noisy rules for the same symptom. |
| MON-NFR-006 | Performance | Monitoring overhead must not materially destabilize the monitored training workload. |
| MON-NFR-007 | Retention | Metric/log retention must be documented and appropriate for the available lab storage. |
| MON-NFR-008 | Portability | The reference implementation should run on a standard Linux VM or equivalent lab environment without proprietary agents. |

## 6. Required incident scenarios

At least two scenarios must be tested:

1. **Service outage:** stop or break the monitored service; verify probe failure, alert, logs/evidence and recovery.
2. **Resource symptom:** create controlled CPU, memory or disk pressure; verify dashboard visibility and alert behavior.

Optional scenarios:
- certificate expiry warning;
- elevated application errors;
- slow endpoint/latency;
- disk-filling condition;
- failed deployment.

## 7. Operational acceptance

The project passes only if the team can diagnose the seeded incident using the monitoring platform without first reading the failure-injection command.
