# Assessment Rubric

Total: **100 points**

| Area | Weight | Full-score standard |
|---|---:|---|
| Discovery and requirements | 10 | SCQ is evidence-based; requirements are prioritized, testable and traceable |
| Solution design | 15 | Architecture is coherent; trade-offs, risks and ADRs are explicit |
| Implementation quality | 15 | Code/config is modular, readable, reviewable and environment-safe |
| Automation and CI/CD | 15 | Build/test/deploy flow is repeatable; no manual hidden steps |
| Testing and data quality | 15 | Positive, negative, integration and acceptance paths are covered |
| Security | 10 | Secrets, identity, input/data handling and dependencies are handled appropriately |
| Observability and operations | 10 | Health, metrics/logs, alerts and runbooks support diagnosis and recovery |
| Documentation and demo | 10 | A new engineer can understand/rebuild the system; demo proves requirements |

## Critical-failure conditions

The following can cap the final score regardless of other quality:

- committed real secrets or private keys;
- production/customer sensitive data in the repository;
- fabricated test evidence;
- inability to run the core workflow;
- no traceability between requirements and delivered behavior;
- implementation copied without team understanding;
- destructive operations with no safeguards in a shared environment.

## Suggested grade bands

- **90-100:** production-minded; strong portfolio evidence.
- **80-89:** solid engineering; minor operational/design gaps.
- **70-79:** functional but important quality/operations gaps remain.
- **60-69:** partial project; weak repeatability or evidence.
- **<60:** core requirements or engineering controls not demonstrated.
