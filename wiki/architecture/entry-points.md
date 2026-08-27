---
title: Entry Points
last_reviewed: 2026-08-27
tags: [architecture, entry-points, startup, handlers]
folder: architecture
sources:
  - code:charts/memgraph/templates/statefulset.yaml
  - code:charts/memgraph-high-availability/templates/data.yaml
  - code:charts/memgraph-high-availability/templates/coordinators.yaml
  - code:charts/memgraph-lab/templates/deployment.yaml
  - code:docker-compose/docker-compose.yml
  - code:scripts/aks.bash
  - code:scripts/aws.bash
  - code:scripts/gke.bash
---

# Entry Points

## Kubernetes Deployment Entry Points

### Helm Install (Primary Entry Point)

Users deploy Memgraph via `helm install` commands from their CLI. This is the primary entry point for all deployment modes.

### Scripts

| Script | Purpose |
| --- | --- |
| `scripts/aks.bash` | Deploy to Azure AKS |
| `scripts/aws.bash` | Deploy to AWS EKS |
| `scripts/gke.bash` | Deploy to Google GKE |
| `scripts/debug-memgraph.sh` | Debug Memgraph pod issues |
| `scripts/find-memgraph-pid.sh` | Find Memgraph process PID for debugging |
| `scripts/aks/` subdirectory | AKS-specific Terraform and deployment resources |

### Docker Compose

`docker-compose/docker-compose.yml` provides a local entry point using Docker Compose for HA cluster testing.

## Container Startup Flow

1. **Init Container (sysctl)**: Sets `vm.max_map_count` kernel parameter for high memory loads
2. **Init Container (core dumps)**: Configures core dump pattern and ptrace scope (optional)
3. **Main Container (Memgraph)**: Starts Memgraph database with configured args
4. **Readiness Probe**: TCP check on Bolt port (7687)
5. **Liveness Probe**: TCP check on Bolt port
6. **Startup Probe**: TCP check on Bolt port (1440 failure threshold ~ 2 hours for backup restore)
