# ProLEAP Academy - Live Projects 2026

This repository holds the live projects for ProLEAP Academy learners working in Cloud, DevOps, Platform Engineering, Automation, Observability and DevSecOps.

## Purpose

Each project runs you through the full engineering lifecycle the way a real team executes it - not a tutorial:

**Discovery -> requirements -> solution intent -> architecture -> implementation -> source control -> CI/CD -> testing -> observability -> security -> operations -> demo -> retrospective**

The target is not "finish a tutorial." The target is a solution that can be explained, rebuilt, tested, operated and demonstrated.

## Projects

Each project draws on specific phases of the [foundation curriculum](docs/00-program-overview.md#relationship-to-the-proleap-devops-learning-path). Use this to check you have the prerequisites before you start.

| # | Project | Foundation phases | Core stack | Level | Main specification |
|---|---|---|---|---|---|
| 1 | **360-Degree Monitoring Platform** | Phase 1 - Bedrock + Phase 4 - Delivery Pipeline | `Linux` `Prometheus` `Node Exporter` `Blackbox Exporter` `Grafana` `Loki` `Alertmanager` `OpenTelemetry` `Runbooks` | Intermediate | [Open project](projects/01-360-degree-monitoring/README.md) |
| 2 | **GitHub Contributor Intelligence Service** | Phase 2 - Scripting & Logic + Phase 3 - Cloud & IaC + Phase 4 - Delivery Pipeline | `Python` `REST API design` `GitHub REST API` `AWS Lambda` `RDS` `Secrets Manager` `IAM` `Async job processing` `GitHub App auth` | Intermediate/Advanced | [Open project](projects/02-github-contributor-intelligence/README.md) |
| 3 | **Dynamic ETL Automation Platform** | Phase 1 - Bedrock + Phase 2 - Scripting & Logic + Phase 3 - Cloud & IaC + Phase 4 - Delivery Pipeline | `Linux` `Bash` `Python` `MySQL` `Secure ingestion (SFTP/HTTPS)` `systemd/cron` `CI/CD` | Intermediate/Advanced | [Open project](projects/03-dynamic-etl/README.md) |
| 4 | **Custom Live Project** | Learner-selected - draws on any phase(s) relevant to the proposal | `Problem discovery` `Architecture design` `Delivery planning` `Documentation` | Variable | [Open project](projects/04-custom-project/README.md) |

## What every team must submit

1. Completed SCQ/discovery document.
2. Solution Intent document approved before implementation.
3. Requirements traceability matrix.
4. Architecture diagram and at least one Architecture Decision Record (ADR).
5. Source code and Infrastructure-as-Code where infrastructure is required.
6. CI/CD pipeline with quality/security checks appropriate to the project.
7. Automated tests plus a documented manual validation plan.
8. Operational dashboards/health checks and actionable alerts where applicable.
9. Runbook covering deployment, rollback, troubleshooting and recovery.
10. Security and data-handling notes.
11. Demo script and evidence.
12. Final retrospective/postmortem-style learning summary.

See [Definition of Done](docs/05-definition-of-done.md) and [Assessment Rubric](docs/04-assessment-rubric.md).

## Delivery workflow

```mermaid
flowchart LR
    A[SCQ Discovery] --> B[Requirements]
    B --> C[Solution Intent]
    C --> D[Architecture & ADRs]
    D --> E[Build in Small Increments]
    E --> F[CI/CD + Tests + Security]
    F --> G[Observability + Runbooks]
    G --> H[UAT / Acceptance Test]
    H --> I[Demo]
    I --> J[Retrospective]
```

### Mandatory gates

- **Gate 1 - Discovery complete:** problem, stakeholders, measurable outcome and constraints are understood.
- **Gate 2 - Design approved:** solution intent, key risks, architecture and acceptance criteria are reviewable.
- **Gate 3 - Build quality:** code is version controlled, testable and deployable through a repeatable process.
- **Gate 4 - Operational readiness:** monitoring, logs, recovery, security and rollback are demonstrated.
- **Gate 5 - Final acceptance:** requirements can be traced to evidence and the team can demo without instructor intervention.

## Repository map

```text
.
|-- README.md
|-- CHANGELOG.md
|-- CONTRIBUTING.md
|-- SECURITY.md
|-- docs/
|   |-- 00-program-overview.md
|   |-- 01-scq-discovery-framework.md
|   |-- 02-solution-intent-guidelines.md
|   |-- 03-delivery-lifecycle.md
|   |-- 04-assessment-rubric.md
|   |-- 05-definition-of-done.md
|   |-- 06-repository-standards.md
|   |-- 07-security-and-data-handling.md
|   |-- 08-ai-use-policy.md
|   |-- 09-modernization-and-traceability.md
|   `-- 10-official-references.md
|-- projects/
|   |-- 01-360-degree-monitoring/
|   |-- 02-github-contributor-intelligence/
|   |-- 03-dynamic-etl/
|   `-- 04-custom-project/
|-- templates/
|-- exports/
|-- legacy/
`-- .github/
```

## Quick start for learners

1. Read [Program Overview](docs/00-program-overview.md).
2. Select one project.
3. Copy the relevant templates from [`templates/`](templates/).
4. Create a new project repository or team branch as instructed by the trainer.
5. Complete SCQ before proposing technology.
6. Complete Solution Intent and obtain design review.
7. Build vertically: get one thin end-to-end path working before expanding features.
8. Commit frequently using small, reviewable changes.
9. Attach evidence to every acceptance criterion.
10. Demo the project from a clean environment or documented deployment procedure.

## Engineering principles

- Prefer **automation over manual steps**.
- Prefer **repeatable infrastructure** over click-only setup.
- Prefer **secure defaults** over retrofitted security.
- Prefer **observable services** over black-box deployments.
- Prefer **idempotent and recoverable processes** over one-shot scripts.
- Prefer **documented trade-offs** over unexplained tool choices.
- Prefer **small, tested increments** over a large final integration.
- Do not hard-code credentials, tokens, IPs, passwords or private keys.
- Do not upload production/customer data to this training repository.

## Choosing your tools

The project specs describe what your solution needs to do, not a fixed list of tools you must use. Pick current, stable releases and write down the exact versions you used in your project's `VERSION_MATRIX.md` or lockfiles.

If a project defines a reference architecture, you may substitute another approach provided you document the trade-off and still meet the acceptance criteria.

## About the older project documents

This repository originates from an earlier, shorter version containing four PDF documents and a brief README. Those originals are preserved under [`legacy/`](legacy/) for reference. The Markdown documents here are the current working specs: they retain the original requirements while adding what the old PDFs left out - API contracts, error handling, observability, security and testing - so each project has enough detail to build against.

To see how a specific old requirement maps to the new docs, check [Modernization and Traceability](docs/09-modernization-and-traceability.md).

PDF versions of the main specs are available under [`exports/`](exports/) for offline reading or printing.

## Questions and changes

This is ProLEAP Academy live-project material, maintained across cohorts. Record any requirement changes in [`CHANGELOG.md`](CHANGELOG.md).
