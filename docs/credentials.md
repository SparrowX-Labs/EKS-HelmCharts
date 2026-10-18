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
```

`ARGOCD_ADMIN_PASSWORD` is the Argo CD local admin password.
`ARGOCD_ADMIN_PASSWORD_MTIME` should contain an RFC3339 timestamp.
Argo CD generates its server secret key when the chart creates `argocd-secret`.

Prometheus is publicly reachable during development and currently has no
built-in login configured. Add an authentication proxy in front of it before
using this setup outside development.

GitHub Actions environment injection is intentionally the simple development
option. Before production, move these values to AWS Secrets Manager plus
External Secrets because Helm release metadata may retain rendered values.
