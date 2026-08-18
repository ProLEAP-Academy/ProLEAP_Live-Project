# Definition of Done

A project is not complete because the code runs once.

## Functional

- [ ] All Must requirements are implemented or formally waived.
- [ ] Acceptance criteria have objective evidence.
- [ ] Error paths are handled deliberately.
- [ ] Inputs are validated.
- [ ] Repeated execution behaves predictably.

## Code and configuration

- [ ] Source is version controlled.
- [ ] No real secrets are stored in Git.
- [ ] Dependency versions are controlled where supported.
- [ ] Configuration is externalized.
- [ ] `.env.example` or equivalent documents required configuration.
- [ ] README contains reproducible setup and run instructions.

## CI/CD

- [ ] Pull/push workflow automatically performs relevant quality checks.
- [ ] Tests run automatically.
- [ ] Security checks appropriate to the stack are present.
- [ ] Deployable artifacts are versioned.
- [ ] Deployment is repeatable.
- [ ] Rollback is documented and tested where practical.

## Infrastructure

- [ ] Required infrastructure is reproducible through IaC or a documented automation path.
- [ ] Network exposure follows least-access principles.
- [ ] Persistent data locations are understood and backed up where required.
- [ ] Resource sizing/limits are documented.

## Testing

- [ ] Unit tests cover important logic.
- [ ] Integration tests cover external boundaries.
- [ ] Negative/failure tests exist.
- [ ] UAT/acceptance test is documented.
- [ ] Performance target is validated if the project defines one.

## Security

- [ ] Secrets use an approved secret-management mechanism.
- [ ] Least privilege is applied.
- [ ] Sensitive data handling is documented.
- [ ] Dependencies/images are scanned where applicable.
- [ ] Inputs and API access are protected.

## Observability

- [ ] Health/status is visible.
- [ ] Important metrics are exposed/collected.
- [ ] Logs are structured enough for diagnosis.
- [ ] Alerts map to real operator actions.
- [ ] Dashboards and runbooks are linked.

## Operations

- [ ] Start, stop, deploy, rollback and recovery procedures exist.
- [ ] Common failures are documented.
- [ ] At least one controlled failure/recovery scenario is demonstrated.
- [ ] Backup/restore is tested if persistent critical data exists.

## Documentation

- [ ] Architecture matches the implementation.
- [ ] Requirements traceability is current.
- [ ] ADRs capture important decisions.
- [ ] Known limitations and future backlog are explicit.
- [ ] Demo instructions work from a clean state.
