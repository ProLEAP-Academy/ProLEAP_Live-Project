# Delivery Lifecycle

## Recommended cadence

The framework is deliberately tool-agnostic. A team can use Scrum, Kanban or a simple milestone board, but work should move through the same engineering gates.

## Stage 1 - Discover

Outputs:
- SCQ;
- stakeholder map;
- current-state notes;
- key constraints;
- initial risk list.

Do not estimate detailed implementation before major unknowns are identified.

## Stage 2 - Define

Outputs:
- business requirements;
- functional and non-functional requirements;
- priorities;
- acceptance criteria;
- requirement traceability matrix.

## Stage 3 - Design

Outputs:
- Solution Intent;
- target architecture;
- data/API contracts;
- ADRs;
- security/reliability/observability design;
- milestone plan.

## Stage 4 - Build vertical slices

Prefer this sequence:

1. establish repository and CI baseline;
2. create minimal deployable environment;
3. implement one thin end-to-end path;
4. add tests and telemetry to that path;
5. expand functionality incrementally;
6. automate deployment and recovery.

Avoid implementing every internal component before proving the end-to-end flow.

## Stage 5 - Verify

Run requirement-based tests. Defects should reference the failed requirement or acceptance criterion.

## Stage 6 - Operationalize

Before final demo, prove:
- startup/deployment;
- health checks;
- dashboard visibility;
- alerting;
- failure diagnosis;
- rollback/recovery;
- backup/restore where applicable;
- secrets are externalized.

## Stage 7 - Accept

The final demo should include:

1. business problem;
2. architecture;
3. normal workflow;
4. requirement evidence;
5. controlled failure;
6. alert/diagnosis;
7. recovery or rollback;
8. known limitations;
9. future backlog.

## Stage 8 - Reflect

Complete a retrospective or postmortem-style summary:
- what worked;
- what failed;
- root causes;
- decisions that changed;
- measurable improvements;
- what would be redesigned next time.
