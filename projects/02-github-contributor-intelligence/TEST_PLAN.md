# GitHub Contributor Intelligence - Test Plan

## Unit tests

- repository/date validation;
- branch-scope validation;
- domain normalization;
- noreply/private-address handling;
- contributor-key selection;
- commit SHA deduplication;
- aggregate counts;
- idempotency-key logic;
- error mapping.

## Integration tests

- GitHub API adapter with paginated responses;
- database create/read/update transaction;
- queue publish/consume;
- Secrets Manager adapter using safe test secret;
- service authentication.

Use mocks/recorded fixtures for most CI tests so the pipeline is deterministic and does not consume GitHub rate limit unnecessarily.

## Contract tests

Validate API requests/responses against OpenAPI or equivalent schema.

## Failure tests

- GitHub 401/403;
- GitHub 404;
- primary/secondary rate limit;
- transient 5xx;
- database unavailable;
- queue retry/redelivery;
- worker termination mid-job.

## Data correctness fixture

Create a deterministic fixture where:

- commit A exists on `main` and `release`;
- commit B exists only on `main`;
- two contributors share a public domain;
- one contributor uses GitHub noreply;
- one commit lacks attributable author data.

Expected summary must be asserted exactly.

## Performance test

Run against a cohort-approved public repository/date range large enough to demonstrate pagination. Measure:

- job duration;
- number of GitHub requests;
- unique commits;
- rate-limit behavior;
- memory use or worker sizing where measurable.
