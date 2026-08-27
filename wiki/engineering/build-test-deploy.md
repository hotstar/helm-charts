---
title: Build, Test, and Deploy
last_reviewed: 2026-08-27
tags: [engineering, build, test, deploy, ci-cd]
folder: engineering
sources:
  - code:charts/memgraph/templates/tests/test-connection.yaml
  - code:CONTRIBUTING.md
  - code:.pre-commit-config.yaml
  - code:lintconf.yaml
---

# Build, Test, and Deploy

## Local Development

### Prerequisites
- Helm 3.x
- Kubernetes cluster (Minikube, kind, or cloud-based)
- kubectl configured

### Chart Linting
The repository uses yamllint for YAML validation, configured in `lintconf.yaml`. Key rules include consistent indentation, Unix line endings, and trailing space detection.

Pre-commit hooks are configured via `.pre-commit-config.yaml` for automated checks.

### Testing

The repository includes a Helm test template for connection testing:
```bash
helm test my-release
```

This runs the test job defined in `charts/memgraph/templates/tests/test-connection.yaml`, which:
1. Connects to the Memgraph Bolt port using mgconsole
2. Runs `RETURN 0;` to verify connectivity
3. Returns success/failure

### Template Validation
```bash
helm template . --debug
helm lint ./charts/memgraph/
helm lint ./charts/memgraph-high-availability/
helm lint ./charts/memgraph-lab/
```

## Deployment

### Standard Deployment
```bash
# Add repository
helm repo add memgraph https://memgraph.github.io/helm-charts
helm repo update

# Install charts
helm install my-release memgraph/memgraph
helm install my-release memgraph/memgraph-lab
helm install my-release memgraph/memgraph-high-availability \
  --set env.MEMGRAPH_ENTERPRISE_LICENSE=<license> \
  --set env.MEMGRAPH_ORGANIZATION_NAME=<org>
```

### Cloud-Specific Deployments
| Cloud | Script | Prerequisites |
| --- | --- | --- |
| AWS EKS | `scripts/aws.bash` | eksctl, aws CLI |
| Azure AKS | `scripts/aks.bash` | az CLI, kubectl |
| GCP GKE | `scripts/gke.bash` | gcloud CLI, kubectl |

### Docker Compose (Local)
```bash
docker compose -f docker-compose/docker-compose.yml up
```

## CI/CD

### Quality Checks
- Pull requests require two code owner approvals
- Tests must pass remotely
- Commits should be atomic (one feature per commit)
- Pre-commit hooks validate YAML and formatting

### Chart Publishing
Charts are packaged as `.tgz` archives and published to the Memgraph Helm repository. The chart index is maintained in `index.yaml` at the repository root. Charts are also discoverable via Artifact Hub.
