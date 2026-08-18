# Security and Data Handling

## Baseline rules

1. Never use real customer/production data unless explicitly authorized for the training environment.
2. Never commit credentials or tokens.
3. Apply least privilege to cloud, database and GitHub access.
4. Encrypt sensitive data in transit and at rest.
5. Validate untrusted inputs.
6. Log security-relevant events without logging secrets.
7. Keep dependencies and base images current and scanned.
8. Remove temporary sensitive files after use where the project requires it.
9. Document data retention and deletion behavior.
10. Use separate credentials/environments for development and demonstration.

## Data classification for projects

Classify each dataset as one of:

- Public
- Internal
- Confidential
- Restricted

If unsure, treat it as Confidential until clarified.

## GitHub-specific privacy

The Contributor Intelligence project must not attempt to de-anonymize users or infer private identity from protected/noreply email addresses. Organization/domain classification may use only data legitimately exposed by the GitHub API and must record uncertainty where attribution is not reliable.

## Logging

Do not log:
- passwords;
- access tokens;
- private keys;
- full authorization headers;
- database credentials;
- sensitive personal fields unless explicitly required and protected.

## Incident handling

If a secret is committed:

1. revoke/rotate it immediately;
2. remove it from active configuration;
3. assess exposure;
4. clean repository history if necessary;
5. document the incident and prevention action.
