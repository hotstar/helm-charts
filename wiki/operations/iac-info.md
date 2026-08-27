---
title: IaC info
last_reviewed: 2026-08-27
tags: [readiness-placeholder, iac-info]
folder: operations
sources:
  - repo-doc:README.md
  - code:charts/memgraph/templates/
  - code:charts/memgraph-high-availability/templates/
  - code:charts/memgraph-lab/templates/
  - code:charts/memgraph/values.yaml
  - code:docker-compose/docker-compose.yml
agent_routing:
  code_change_relevance: conditional
  task_intents: [infrastructure-change]
  applies_to_paths:
    - charts/**
    - docker-compose/**
  applies_to_symbols: []
---

# IaC info

> Readiness page: generated from repo evidence for `iac-info` and still needs human review.

## Repository Overview

This is a Helm chart repository for deploying Memgraph on Kubernetes. It provides three charts:
- **memgraph** — standalone Memgraph database deployment
- **memgraph-lab** — Memgraph Lab visualization tool
- **memgraph-high-availability** — HA Memgraph cluster (Enterprise)

## Kubernetes Resources Managed

### Memgraph standalone (`charts/memgraph/templates/`)
- StatefulSet with init containers for sysctl configuration and core dumps
- Services (ClusterIP + optional LoadBalancer)
- Service Account
- StorageClass (optional)
- Prometheus exporter deployment
- ServiceMonitor for Prometheus operator

### Memgraph High Availability (`charts/memgraph-high-availability/templates/`)
- Coordinator and data instance StatefulSets
- External and internal services for coordinators and data
- Cluster setup job
- Ingress-Nginx configuration
- Prometheus exporter

### Memgraph Lab (`charts/memgraph-lab/templates/`)
- Deployment (not stateful — Lab is stateless)
- Service

## Cloud Infrastructure

The repository includes cloud-specific deployment guides and infrastructure:
- **AWS**: Cluster setup guide and CloudFormation/YAML templates under `charts/memgraph-high-availability/aws/`
- **Azure/AKS**: Terraform scripts under `charts/memgraph-high-availability/aks/` including `main.tf`, `outputs.tf`, `variables.tf`

## Docker Compose

A Docker Compose file under `docker-compose/docker-compose.yml` provides local HA cluster deployment using Docker bridge networking.

## Infrastructure-as-Code Details

- Charts follow standard Helm chart structure with `Chart.yaml`, `values.yaml`, `templates/`
- Charts are published to Artifact Hub: `https://artifacthub.io/packages/search?repo=memgraph`
- Helm package index maintained at `index.yaml` in repo root
- YAML linting configured via `lintconf.yaml`

## Source References

- `README.md` — contributed chart overview and deployment instructions.
- `charts/memgraph/templates/` — contributed all K8s resource definitions for standalone chart.
- `charts/memgraph-high-availability/templates/` — contributed HA cluster K8s resources.
- `charts/memgraph/values.yaml` — contributed all configurable parameters.
- `charts/memgraph-high-availability/aks/main.tf` — contributed Terraform infrastructure for AKS deployment.
- `docker-compose/docker-compose.yml` — contributed local Docker-based deployment.

## Suggested Content

- Add detailed networking configuration (ingress, TLS, network policies).
- Add backup and restore procedures for persistent data.
- Add disaster recovery documentation.
- Document storage class options and provisioning across cloud providers.
