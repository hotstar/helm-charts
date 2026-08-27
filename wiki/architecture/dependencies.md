---
title: Dependencies
last_reviewed: 2026-08-27
tags: [architecture, dependencies, external]
folder: architecture
sources:
  - code:charts/memgraph/values.yaml
  - code:charts/memgraph-high-availability/values.yaml
  - code:charts/memgraph-lab/values.yaml
  - code:charts/memgraph/Chart.yaml
---

# Dependencies

## External Container Images

| Image | Repository | Default Tag | Used By |
| --- | --- | --- | --- |
| Memgraph | `docker.io/memgraph/memgraph` | Chart appVersion | Standalone and HA charts |
| Memgraph Lab | `docker.io/memgraph/lab` | Chart appVersion | Lab chart |
| Busybox (sysctl) | `docker.io/library/busybox` | `latest` | Standalone chart init container |
| Prometheus Exporter | `docker.io/memgraph/prometheus-exporter` | `0.2.1` | Standalone and HA monitoring |

## Kubernetes Dependencies

| Component | Requirement |
| --- | --- |
| Kubernetes cluster | 1.19+ (recommended) |
| Helm | 3.x |
| StorageClass | default or custom provisioned |
| Prometheus Operator | Required only when ServiceMonitor is enabled |
| Ingress-Nginx | Required only for HA ingress configuration |

## Cloud Provider Dependencies

| Provider | Script/Config | Dependencies |
| --- | --- | --- |
| AWS EKS | `scripts/aws.bash`, `charts/memgraph-high-availability/aws/` | eksctl, aws CLI, kubectl |
| Azure AKS | `scripts/aks.bash`, Terraform in `charts/memgraph-high-availability/aks/` | az CLI, Terraform, kubectl |
| GCP GKE | `scripts/gke.bash` | gcloud CLI, kubectl |

## No Vendor Lock-in

The chart has no direct Helm chart dependencies (the `dependencies` field in Chart.yaml is empty). All infrastructure requirements are satisfied by the target Kubernetes cluster capabilities.

## Build Tools

- **Helm**: Chart packaging and deployment (v3+)
- **yamllint**: Configuration validation via `lintconf.yaml`
- **pre-commit**: Automated pre-commit checks via `.pre-commit-config.yaml`
