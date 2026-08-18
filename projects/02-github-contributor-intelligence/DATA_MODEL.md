# GitHub Contributor Intelligence - Logical Data Model

The legacy requirement suggested one table. The modern design separates job state from normalized results so reruns, troubleshooting and future extensions remain manageable.

## `analysis_job`

| Column | Purpose |
|---|---|
| `id` | Unique analysis ID |
| `requester_id` | Authenticated caller/user/service where available |
| `repository_owner` | GitHub owner |
| `repository_name` | GitHub repository |
| `since_ts` | Inclusive analysis start |
| `until_ts` | Inclusive/exclusive behavior must be documented consistently |
| `branch_scope_json` | Requested branch policy/list |
| `status` | queued/running/completed/partial/failed |
| `created_at` | Request time |
| `started_at` | Worker start |
| `completed_at` | Terminal time |
| `error_code` | Sanitized terminal error if any |
| `error_message` | Sanitized diagnostic summary |
| `idempotency_key` | Prevent accidental duplicate request creation |

## `analysis_branch`

Stores discovered/processed branches and progress.

## `analysis_commit`

Minimum fields:

- analysis_id;
- commit_sha;
- authored/committed timestamp chosen by documented rule;
- GitHub author ID/login when available;
- normalized contributor key;
- public email/domain if legitimately available;
- attribution source/confidence.

Unique constraint should prevent duplicate `(analysis_id, commit_sha)` records.

## `analysis_domain_summary`

| Column | Purpose |
|---|---|
| `analysis_id` | Parent job |
| `domain` | Normalized domain or special `unattributed` category |
| `total_commits` | Deduplicated commit count |
| `unique_contributors` | Distinct normalized contributor count |
| `attribution_source` | Classification source/rule |

## Data-retention decision

The Solution Intent must state whether raw per-commit rows are retained permanently, retained temporarily for audit/troubleshooting, or deleted after summary generation. Training projects should minimize unnecessary personal data retention.
