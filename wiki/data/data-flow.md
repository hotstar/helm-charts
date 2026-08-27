---
title: Data Flow
last_reviewed: 2026-08-27
tags: [data, flow, communication, monitoring]
folder: data
sources:
  - code:charts/memgraph/templates/statefulset.yaml
  - code:charts/memgraph/templates/service.yaml
  - code:charts/memgraph/templates/mg-exporter.yaml
  - code:charts/memgraph-high-availability/templates/data.yaml
  - code:charts/memgraph-high-availability/templates/coordinators.yaml
  - code:docker-compose/docker-compose.yml
---

# Data Flow

## Query Flow (Standalone)

```
Client (mgconsole, Lab, App)
  |
  | Bolt protocol (TCP/7687)
  v
Kubernetes Service (ClusterIP or LoadBalancer)
  |
  v
Memgraph Pod (StatefulSet)
  |-- Read/Write data
  |-- In-memory graph processing
  v
Persistent Storage (PVC)
  |-- Snapshot writes (every 300s)
  |-- WAL writes
  |-- Recovery reads on startup
```

## Query Flow (HA Cluster)

```
Client
  |
  | Bolt protocol
  v
Coordinator Pods (x3, raft consensus)
  |-- Route queries to appropriate data instance
  |-- Maintain cluster membership
  |
  v
Data Pods (x2)
  |-- Primary handles writes
  |-- Replica handles reads (configurable)
  |
  v
Persistent Storage (PVC per instance)
```

## Metrics Flow (Prometheus)

```
Memgraph Pod (port 9091)
  |
  | HTTP metrics endpoint
  v
Prometheus Exporter (mg-exporter Deployment, port 9115)
  |-- Pulls metrics from Memgraph every 5 seconds
  |
  | Prometheus scrape (ServiceMonitor, every 15s)
  v
Prometheus / kube-prometheus-stack
```

## Replication Flow (HA)

```
Coordinator Leader
  |
  +--> Data Instance 1 (primary)
  |      |-- Replication
  |      v
  |      Data Instance 2 (replica)
  |
  +--> Coordinator 2 (follower)
  +--> Coordinator 3 (follower)

Replica check interval: 1 second
```

## Data Flow Through Docker Compose

```
docker-compose/
  |-- HA cluster on Docker bridge network
  |-- Uses license.cypher and HA_register.cypher to
  |   initialize and register HA cluster members
```

## Certificate and Secret Flow

```
Kubernetes Secret (memgraph-secrets)
  |
  | Injected as env vars
  v
Memgraph Container
  |-- MEMGRAPH_USER, MEMGRAPH_PASSWORD
  |-- MEMGRAPH_ENTERPRISE_LICENSE
  |-- MEMGRAPH_ORGANIZATION_NAME
```
