---
title: Module Structure
last_reviewed: 2026-08-27
tags: [architecture, helm, chart-structure, modules]
folder: architecture
sources:
  - code:charts/memgraph/
  - code:charts/memgraph-high-availability/
  - code:charts/memgraph-lab/
  - code:docker-compose/
  - code:scripts/
---

# Module Structure

The repository is organized into three distinct Helm charts plus supporting infrastructure.

## Chart Modules

### Standalone Memgraph Chart (`charts/memgraph/`)

Deploys a single Memgraph instance as a Kubernetes StatefulSet. Key components:
- **StatefulSet** (`templates/statefulset.yaml`) — manages the Memgraph pod with init containers for sysctl configuration and core dumps, volume claim templates for persistent storage
- **Service** (`templates/service.yaml`) — ClusterIP service for Bolt protocol (7687), WebSocket monitoring (7444), and HTTP monitoring (9091)
- **LoadBalancer Service** (`templates/service-loadbalancer.yaml`) — optional external-facing service for cluster-external access
- **ServiceAccount** (`templates/serviceaccount.yaml`) — RBAC identity for the pod
- **StorageClass** (`templates/storageclass.yaml`) — optional custom storage class
- **Prometheus Exporter** (`templates/mg-exporter.yaml`) — ConfigMap, Deployment, Service, and ServiceMonitor for Prometheus metrics
- **Connection Test** (`templates/tests/test-connection.yaml`) — Helm test job for verifying pod connectivity
- **Helpers** (`templates/_helpers.tpl`) — reusable name, label, and probe templates

### High Availability Chart (`charts/memgraph-high-availability/`)

Deploys an HA Memgraph cluster for enterprise users. Key components:
- **Data StatefulSets** (`templates/data.yaml`) — two data instance pods with persistent storage
- **Coordinator StatefulSets** (`templates/coordinators.yaml`) — three coordinator pods for cluster coordination
- **Internal and External Services** (`templates/services-data.yaml`, `templates/services-coordinators.yaml`, `templates/services-data-external.yaml`, `templates/services-coordinators-external.yaml`) — both internal and external networking
- **Cluster Setup** (`templates/cluster-setup.yaml`) — initialization job for HA cluster registration
- **Ingress-Nginx** (`templates/ingress-nginx.yaml`) — optional ingress controller configuration
- **Prometheus Exporter** (`templates/mg-exporter.yaml`) — monitoring support
- **Helpers** (`templates/_helpers.tpl`) — reusable templates including core dump uploader sidecar

### Memgraph Lab Chart (`charts/memgraph-lab/`)

Deploys the Memgraph Lab visualization web interface. Key components:
- **Deployment** (`templates/deployment.yaml`) — stateless deployment of the Lab web UI
- **Service** (`templates/service.yaml`) — ClusterIP service exposing port 3000
- **Ingress** (`templates/ingress.yaml`) — optional ingress for external access
- **HPA** (`templates/hpa.yaml`) — optional horizontal pod autoscaler
- **ServiceAccount** (`templates/serviceaccount.yaml`) — RBAC identity

## Supporting Modules

| Module | Purpose |
| --- | --- |
| `docker-compose/` | Local development and testing with Docker Compose (HA cluster) |
| `scripts/` | Cloud deployment scripts (aks.bash, aws.bash, gke.bash), debugging (debug-memgraph.sh, find-memgraph-pid.sh), and performance test pod definition |
| `tutorials/` | Platform-specific guides with symlinks to HA chart documentation |

## Cloud Infrastructure Modules

| Path | Purpose |
| --- | --- |
| `charts/memgraph-high-availability/aws/` | AWS EKS deployment guide and cluster.yaml |
| `charts/memgraph-high-availability/aks/` | Azure AKS deployment with Terraform (main.tf, variables.tf, outputs.tf) |
