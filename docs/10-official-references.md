# Official Technical References

Checked during the 2026 modernization pass. Project teams should re-check current documentation when implementing because services and limits can change.

## GitHub

- GitHub REST API: https://docs.github.com/en/rest
- REST API best practices: https://docs.github.com/en/rest/using-the-rest-api/best-practices-for-using-the-rest-api
- REST API rate limits: https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api
- Repository commits API: https://docs.github.com/en/rest/commits/commits
- Repository branches API: https://docs.github.com/en/rest/branches/branches
- GitHub App authentication: https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app

## AWS

- AWS Well-Architected Framework: https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html
- AWS Secrets Manager best practices: https://docs.aws.amazon.com/secretsmanager/latest/userguide/best-practices.html
- Lambda with RDS: https://docs.aws.amazon.com/lambda/latest/dg/services-rds.html
- Amazon RDS Proxy: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html
- RDS for MySQL version management: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MySQL.Concepts.VersionMgmt.html
- API Gateway request throttling: https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html

## Observability

- Prometheus overview: https://prometheus.io/docs/introduction/overview/
- Prometheus alerting practices: https://prometheus.io/docs/practices/alerting/
- Prometheus Node Exporter guide: https://prometheus.io/docs/guides/node-exporter/
- Alertmanager: https://prometheus.io/docs/alerting/latest/alertmanager/
- Grafana Loki: https://grafana.com/docs/loki/latest/
- Grafana provisioning: https://grafana.com/docs/grafana/latest/administration/provisioning/
- OpenTelemetry Collector: https://opentelemetry.io/docs/collector/

## General rule

Do not copy version numbers from this repository into production blindly. Pin and test versions in the implementation repository, and document upgrade decisions.
