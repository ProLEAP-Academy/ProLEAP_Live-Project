# Repository Standards

## 1. Branching

Recommended for student teams:

- `main` - accepted, demonstrable state;
- short-lived feature branches;
- pull requests for material changes.

Avoid long-running personal branches that are integrated only at the end.

## 2. Commit style

Prefer small commits with an imperative subject.

Examples:

```text
feat: add ETL run manifest and checksum validation
fix: deduplicate commits across GitHub branches
ops: add alert for failed ingestion jobs
docs: record decision to use SFTP instead of FTP
test: cover same-day rerun idempotency
```

## 3. Pull requests

Each PR should state:
- problem/change;
- requirement IDs affected;
- test evidence;
- operational/security impact;
- rollback note if deployment behavior changes.

## 4. Configuration

- No credentials in code.
- Use environment variables or configuration files for deploy-time values.
- Provide safe examples.
- Validate required configuration at startup.

## 5. Documentation

Prefer Markdown and Mermaid so documentation changes can be reviewed in Git.

## 6. Versioning

Use semantic versioning for released application artifacts where practical:

`MAJOR.MINOR.PATCH`

Record exact runtime/tool versions in `VERSION_MATRIX.md` or lockfiles rather than relying on "latest" in deployment code.

## 7. Project README minimum

Every implementation repo should include:

1. purpose;
2. architecture summary;
3. prerequisites;
4. local setup;
5. configuration;
6. test commands;
7. run/deploy commands;
8. troubleshooting;
9. known limitations;
10. links to Solution Intent, runbook and acceptance evidence.
