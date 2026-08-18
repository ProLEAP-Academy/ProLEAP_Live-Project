# GitHub Contributor Intelligence - API Specification

Base path: `/v1`

This document defines the minimum contract. Teams may implement OpenAPI 3.x from this specification.

## 1. Create analysis

`POST /v1/analyses`

### Headers

```text
Authorization: Bearer <service-token>
Idempotency-Key: <client-generated-key>
Content-Type: application/json
```

### Request

```json
{
  "repository": "hashicorp/consul",
  "since": "2026-07-01T00:00:00Z",
  "until": "2026-07-31T23:59:59Z",
  "branch_scope": "all"
}
```

Alternative explicit branches:

```json
{
  "repository": "owner/repo",
  "since": "2026-07-01T00:00:00Z",
  "until": "2026-07-31T23:59:59Z",
  "branch_scope": ["main", "release/1.x"]
}
```

### Response

`202 Accepted`

```json
{
  "analysis_id": "01J...",
  "status": "queued",
  "status_url": "/v1/analyses/01J..."
}
```

## 2. Get analysis status

`GET /v1/analyses/{analysis_id}`

```json
{
  "analysis_id": "01J...",
  "repository": "hashicorp/consul",
  "status": "running",
  "created_at": "2026-08-18T01:00:00Z",
  "started_at": "2026-08-18T01:00:02Z",
  "completed_at": null,
  "progress": {
    "branches_discovered": 14,
    "branches_processed": 7,
    "unique_commits_processed": 1274
  }
}
```

Terminal states:

- `completed`
- `partial`
- `failed`
- `cancelled` (optional)

## 3. Get summary

`GET /v1/analyses/{analysis_id}/summary`

`200 OK`

```json
{
  "analysis_id": "01J...",
  "repository": "hashicorp/consul",
  "period": {
    "since": "2026-07-01T00:00:00Z",
    "until": "2026-07-31T23:59:59Z"
  },
  "unique_commits": 1520,
  "unique_contributors": 94,
  "domains": [
    {
      "domain": "example.com",
      "total_commits": 50,
      "unique_contributors": 10,
      "attribution_source": "public-email-domain"
    }
  ],
  "unattributed": {
    "total_commits": 120,
    "unique_contributors": 18
  }
}
```

## 4. Error format

```json
{
  "error": {
    "code": "GITHUB_RATE_LIMITED",
    "message": "Upstream provider temporarily rate limited the analysis.",
    "request_id": "req_...",
    "retryable": true
  }
}
```

Minimum error codes:

- `INVALID_REQUEST`
- `UNAUTHORIZED`
- `FORBIDDEN`
- `REPOSITORY_NOT_FOUND`
- `GITHUB_AUTH_FAILED`
- `GITHUB_RATE_LIMITED`
- `ANALYSIS_NOT_FOUND`
- `ANALYSIS_FAILED`
- `INTERNAL_ERROR`

Do not return provider tokens, raw stack traces or secrets in API errors.

## 5. Validation rules

- repository must match a safe `owner/repo` form;
- `since < until`;
- date range must be within a cohort-defined maximum, e.g. 366 days unless explicitly overridden;
- explicit branch list must have a defined maximum;
- unknown fields should be rejected or ignored consistently and documented.

## 6. Pagination of result data

If contributor/domain result sets become large, add `limit` and cursor/page semantics. Do not silently truncate output.
