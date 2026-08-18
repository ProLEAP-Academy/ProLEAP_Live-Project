# Project 02 - GitHub Contributor Intelligence Service

## Project statement

Build a secure API service that analyzes one or more user-specified GitHub repositories for a date range and produces contributor/domain-level contribution statistics without double-counting commits that are reachable from multiple branches.

This is the modernized successor to the legacy **GitHub Aggregator** project.

## Core outcome

Given a repository such as `hashicorp/consul` and a date range, the service should create a repeatable analysis job and return a normalized summary such as:

```json
{
  "repository": "hashicorp/consul",
  "period": {
    "since": "2026-07-01T00:00:00Z",
    "until": "2026-07-31T23:59:59Z"
  },
  "domains": [
    {
      "domain": "example.com",
      "total_commits": 50,
      "unique_contributors": 10,
      "attribution_confidence": "public-email-domain"
    }
  ]
}
```

Actual results depend on information exposed by GitHub. The service must not attempt to reverse protected/noreply identities.

## Why the architecture is asynchronous

A repository can contain many branches and commits. Analysis can require pagination, deduplication and rate-limit-aware retries. A production-minded design should therefore create a job and let workers process it rather than forcing all work into one synchronous API request.

## Required artifacts

- [Business Requirements](BUSINESS_REQUIREMENTS.md)
- [Architecture](ARCHITECTURE.md)
- [API Specification](API_SPECIFICATION.md)
- [Data Model](DATA_MODEL.md)
- [Acceptance Criteria](ACCEPTANCE_CRITERIA.md)
- [Test Plan](TEST_PLAN.md)
- Completed SCQ and Solution Intent
- IaC for AWS reference deployment
- CI/CD pipeline
- Runbook

## Recommended implementation profile

- API Gateway HTTP or REST API;
- compute for API handler;
- SQS or equivalent job queue;
- worker compute (Lambda for bounded workloads or container worker for longer jobs);
- Amazon RDS MySQL 8.4 or another approved relational engine;
- RDS Proxy when Lambda/database connection patterns justify it;
- AWS Secrets Manager for application/GitHub credentials;
- CloudWatch or equivalent for operational telemetry;
- GitHub App installation authentication for GitHub API access.

Alternative AWS components are allowed if trade-offs are documented.
