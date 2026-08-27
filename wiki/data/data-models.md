---
title: Data Models and Schemas
last_reviewed: 2026-08-27
tags: [data, schema, storage, helm]
folder: data
sources:
  - code:charts/memgraph/values.yaml
  - code:charts/memgraph/memgraph.conf
  - code:charts/memgraph-high-availability/values.yaml
---

# Data Models and Schemas

## Memgraph Database Storage Model

Memgraph is an in-memory graph database that stores data in a property graph model. Key storage characteristics derived from repository configuration:

### Storage Locations
- **Data directory**: `/var/lib/memgraph` (mounted from PVC)
- **Log directory**: `/var/log/memgraph` (optional PVC)
- **Query modules**: `/usr/lib/memgraph/query_modules`

### Persistence Configuration
- **Snapshot interval**: 300 seconds (configurable)
- **Snapshots on exit**: Enabled
- **Snapshot retention**: 3 snapshots
- **WAL (Write-Ahead Log)**: Enabled
- **Recovery on startup**: Enabled
- **Items per batch**: 1,000,000 (snapshot file batching)

### Storage Classes
The repository can create a custom StorageClass or use the cluster default. Default configuration targets Minikube:
- **Provisioner**: `k8s.io/minikube-hostpath`
- **Reclaim policy**: `Retain`
- **Volume binding mode**: `Immediate`

### Data Dependencies
- **PVC size**: 10Gi (data), 1Gi (logs), 1Gi (user data)
- **Access modes**: ReadWriteOnce for data and logs, configurable for user storage
- **Core dumps**: Optional 10Gi PVC at `/var/core/memgraph`

## HA Cluster Data Architecture

The HA chart manages two distinct StatefulSet types:
- **Data instances**: Store and serve graph data (2 pods by default)
- **Coordinators**: Manage cluster state and routing (3 pods by default)

Each data instance has its own PVC for lib storage and logs. Coordinators also maintain independent storage for cluster metadata.

## Helm Chart Data Model

The repository itself uses a chart package data model:
- **Chart.yaml**: Metadata (name, version, appVersion, description, sources)
- **values.yaml**: Default configuration values (the primary API surface)
- **templates/**: Go-templated Kubernetes resource manifests
- **index.yaml**: Repository-level chart index for Helm discovery

## Query Module Integration

Custom Cypher query modules can be mounted into Memgraph pods via ConfigMaps:
- Mount path: `/var/lib/memgraph/internal_modules/<filename>`
- Supports Python or shared library query modules
