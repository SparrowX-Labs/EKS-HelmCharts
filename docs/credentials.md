# Credential management

For development, credentials are supplied as GitHub Actions secrets and exposed
to Helmfile only as environment variables. Do not print these variables in CI
logs or commit them to this repository.

Required GitHub Actions secrets/environment variables:

```text
ARGOCD_ADMIN_PASSWORD
ARGOCD_ADMIN_PASSWORD_MTIME
GRAFANA_ADMIN_USER
GRAFANA_ADMIN_PASSWORD
PROMETHEUS_ADMIN_USER
PROMETHEUS_ADMIN_PASSWORD
```

`ARGOCD_ADMIN_PASSWORD` is the Argo CD local admin password.
`ARGOCD_ADMIN_PASSWORD_MTIME` should contain an RFC3339 timestamp.
Argo CD generates its server secret key when the chart creates `argocd-secret`.

The chart generates Prometheus' `web.yml` and bcrypt hash from
`PROMETHEUS_ADMIN_USER` and `PROMETHEUS_ADMIN_PASSWORD`; no Prometheus config
needs to be supplied as a GitHub secret.

Prometheus is publicly reachable during development, but the UI and API require
these credentials. Prometheus documents this `web.config.file` authentication
mechanism at https://prometheus.io/docs/guides/basic-auth/.

GitHub Actions environment injection is intentionally the simple development
option. Before production, move these values to AWS Secrets Manager plus
External Secrets because Helm release metadata may retain rendered values.
