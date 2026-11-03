# EKS platform Helm charts

Cluster-level Helmfile environments and supporting charts for the SparrowX Kubernetes platform.

## Contents

- `environments/dev` and `environments/prod`: Helmfile templates for Argo CD, Crossplane/providers, Gateway API CRDs, Traefik, monitoring, External Secrets, DNS, and cluster services.
- `charts/`: local charts for Crossplane providers, Gateway API CRDs, and storage classes.
- `.github/workflows/`: change detection, plan, and apply workflows.

`dev` and `prod` are separate namespaces and release values on one EKS cluster. Cluster-scoped components such as Crossplane and CRDs are installed once; environment-specific application resources are separated by namespace and Argo CD application.

## GitHub Actions configuration

This repository has separate repository-level variables: `AWS_ACCOUNT_ID`, `AWS_REGION`, `AWS_ROLE_NAME`, `DEV_EKS_CLUSTER_NAME`, `PROD_EKS_CLUSTER_NAME`, `DEV_ACM_CERTIFICATE_ARN`, `PROD_ACM_CERTIFICATE_ARN`, `DEV_PUBLIC_DNS_DOMAIN`, `PROD_PUBLIC_DNS_DOMAIN`, `DEV_ARGOCD_PUBLIC_HOSTNAME`, `PROD_ARGOCD_PUBLIC_HOSTNAME`, `DEV_GRAFANA_PUBLIC_HOSTNAME`, `PROD_GRAFANA_PUBLIC_HOSTNAME`, `DEV_PROMETHEUS_PUBLIC_HOSTNAME`, `PROD_PROMETHEUS_PUBLIC_HOSTNAME`, and `GRAFANA_ADMIN_USER`.

The workflows consume organization secrets `ARGOCD_ADMIN_PASSWORD_HASH`, `ARGOCD_ADMIN_PASSWORD_MTIME`, and `GRAFANA_ADMIN_PASSWORD`. The AWS role must be trusted for this repository’s GitHub OIDC subject and be authorized to update EKS and install Helm releases.

## License

See [LICENSE.md](LICENSE.md).
