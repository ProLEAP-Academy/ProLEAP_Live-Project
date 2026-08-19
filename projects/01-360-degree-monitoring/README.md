# Project 01 - 360-Degree Monitoring Platform

## Project statement

Design and implement an end-to-end observability platform for one or more Linux-hosted services so that an operator can answer:

- Is the service available?
- Is the host healthy?
- Is the application healthy?
- What changed before the failure?
- What logs, metrics and traces explain the failure?
- Who should be alerted?
- What action should the operator take?

The project must move beyond "install Grafana" and demonstrate monitoring as an operational system.

## Recommended reference stack

A reference open-source stack is:

- Prometheus for metrics collection/querying;
- Node Exporter for Linux host metrics;
- Blackbox Exporter for endpoint/synthetic probes;
- Grafana for dashboards;
- Loki for centralized logs;
- Grafana Tempo (or Jaeger) for distributed traces, correlated with logs and metrics via Grafana;
- Alertmanager and/or Grafana Alerting for notification routing;
- OpenTelemetry Collector as the vendor-neutral receiver/processor for application metrics, logs and traces.

Alternatives are allowed if the same capabilities and acceptance criteria are met.

## Required artifacts

- [Business Requirements](BUSINESS_REQUIREMENTS.md)
- [Architecture](ARCHITECTURE.md)
- [Acceptance Criteria](ACCEPTANCE_CRITERIA.md)
- [Test Plan](TEST_PLAN.md)
- Completed SCQ and Solution Intent
- Infrastructure/deployment automation
- Dashboard definitions stored in version control where practical
- Alert rules stored in version control
- Runbook(s)
- Final demo evidence

## Minimum demo

The team must demonstrate:

1. healthy host/application;
2. CPU/memory/disk/network or equivalent host visibility;
3. application/endpoint availability;
4. centralized log search;
5. one threshold/symptom alert;
6. one controlled incident;
7. alert delivery;
8. diagnosis using telemetry;
9. recovery and alert resolution;
10. runbook execution.

## Stretch goals

- trace-to-log-to-metric correlation across multiple services, not just one;
- SLO/error-budget dashboard;
- multi-host discovery;
- Kubernetes deployment;
- HA monitoring components;
- remote storage;
- synthetic user journey;
- automated incident annotation from deployments.
