# Security Policy

## Training data only

Do not commit production credentials, customer data, real personal data, private repository tokens, SSH private keys, cloud access keys or database dumps.

## Secrets

- Store local secrets in ignored `.env` files or a secret manager.
- Provide only `.env.example` files with placeholder values.
- Rotate any secret that is accidentally committed, even if the commit is later removed.
- Use least-privilege credentials for demos.

## Vulnerability reporting

If a vulnerability affects shared ProLEAP Academy infrastructure or exposes credentials/data, report it privately to the repository/course maintainers. Do not publish exploitable details in a public issue before remediation.

## Dependency hygiene

Projects should use dependency lockfiles where supported and include automated dependency/security scanning appropriate to the chosen language and platform.
