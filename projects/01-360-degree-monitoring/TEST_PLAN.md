# 360-Degree Monitoring - Test Plan

## Functional tests

1. Verify all monitoring components start successfully.
2. Verify Prometheus targets are healthy.
3. Verify host metrics are queryable.
4. Verify endpoint probe succeeds when application is healthy.
5. Verify logs arrive in the configured backend.
6. Verify dashboards load from provisioned configuration.

## Failure injection

### Scenario A - service unavailable

- stop the service or block its serving port;
- capture time of injection;
- verify probe failure;
- verify alert firing;
- use logs/metrics to diagnose;
- restore service;
- verify alert resolution.

### Scenario B - resource pressure

Use a safe lab-only load generator or controlled disk allocation. Never run destructive stress tests on shared/production systems.

Verify:
- metric increase;
- threshold duration behavior;
- alert;
- recovery.

## Persistence/rebuild test

Recreate the monitoring stack from repository configuration and verify dashboards/alerts return without manual GUI reconstruction.

## Security test

- run a secret scan;
- verify no unauthenticated administrative interface is intentionally exposed to the public network;
- verify test notification credentials are externalized.
