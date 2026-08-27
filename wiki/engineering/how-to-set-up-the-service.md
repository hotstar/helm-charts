---
title: How to set up the service
last_reviewed: 2026-08-27
tags: [readiness-placeholder, service-setup]
folder: engineering
sources:
  - repo-doc:README.md
  - repo-doc:charts/memgraph/README.md
  - repo-doc:charts/memgraph-lab/README.md
  - repo-doc:charts/memgraph-high-availability/README.md
  - code:charts/memgraph/values.yaml
agent_routing:
  code_change_relevance: conditional
  task_intents: [repo-onboarding]
  applies_to_paths: []
  applies_to_symbols: []
---

# How to set up the service

> Readiness page: generated from repo evidence for `service-setup` and still needs human review.

## Prerequisites

- Helm version 3 or above installed.
- Kubernetes cluster (Minikube, cloud-based, or equivalent).

## Add the Helm repository

```bash
helm repo add memgraph https://memgraph.github.io/helm-charts
helm repo update
```

## Install Memgraph standalone

```bash
helm install my-release memgraph/memgraph
```

Replace `my-release` with a name of your choice for the release.

## Install Memgraph Lab

```bash
helm install my-release memgraph/memgraph-lab
```

## Install Memgraph high availability (Enterprise)

```bash
helm install my-release memgraph/memgraph-high-availability --set env.MEMGRAPH_ENTERPRISE_LICENSE=<your-license>,env.MEMGRAPH_ORGANIZATION_NAME=<your-organization-name>
```

## Changing default chart values

```bash
helm install my-release memgraph/memgraph --set <flag1>=<value1>,<flag2>=<value2>,...
```

Or use a custom values file:

```bash
helm install my-release memgraph/memgraph -f values.yaml
```

## Configuration

The Helm chart supports extensive configuration through `values.yaml` files. Key configuration areas include:
- Image repository and tags for Memgraph, Memgraph Lab, and Busybox containers
- Service types: ClusterIP, NodePort, LoadBalancer
- Persistent volume claims for storage, logs, user data, and core dumps
- Storage class provisioning
- Resource limits and requests
- Security contexts, probes, and init containers
- Prometheus exporter monitoring
- Kubernetes secrets for authentication

## Source References

- `README.md` — contributed Helm repo setup and chart installation commands.
- `charts/memgraph/README.md` — contributed detailed configuration options for standalone chart.
- `charts/memgraph-lab/README.md` — contributed Lab chart configuration.
- `charts/memgraph-high-availability/README.md` — contributed HA cluster setup instructions.
- `charts/memgraph/values.yaml` — contributed all configurable parameters and their defaults.

## Suggested Content

- Add Docker Compose setup instructions for local non-Kubernetes development.
- Add step-by-step guide for configuring and creating storage classes.
- Add instructions for configuring Prometheus monitoring integration.
- Add local service reset steps and troubleshooting.
- Add multi-cloud deployment considerations (AWS, GCP, Azure).
