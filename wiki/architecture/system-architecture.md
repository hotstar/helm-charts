---
title: Architecture
last_reviewed: 2026-08-27
tags: [architecture, service-boundaries, component-relationships]
folder: architecture
sources:
  - code:charts/memgraph/templates/statefulset.yaml
  - code:charts/memgraph-high-availability/templates/data.yaml
  - code:charts/memgraph-high-availability/templates/coordinators.yaml
  - code:charts/memgraph-high-availability/templates/cluster-setup.yaml
  - code:docker-compose/docker-compose.yml
---

# Architecture

## System Components

### Standalone Mode

```
User/Frontend (Bolt protocol)
       |
       v
+------------------+
|  K8s Service     |  (ClusterIP / LoadBalancer)
|  ports: 7687     |
+------------------+
       |
       v
+--------------------------+
|  StatefulSet (1 replica) |
|  Memgraph Container      |
|  + Sysctl Init Container |
|  + Core Dump Init (opt)  |
+--------------------------+
       |
+------------------+   +------------------+
| PVC (lib) 10Gi   |   | PVC (logs) 1Gi   |
+------------------+   +------------------+
       |
+-------------------------+
| Prometheus Exporter     |
| (optional)              |
| Deployment + Service    |
| ServiceMonitor          |
+-------------------------+
```

### High Availability Mode (Enterprise)

```
Clients (Bolt)
      |
      v
+----------------------------+
| Coordinator Pods (x3)      |
| StatefulSet, raft-based    |
| consensus for cluster mgmt |
+----------------------------+
      |
      v
+----------------------------+
| Data Pods (x2)             |
| StatefulSet, primary/replica|
+----------------------------+
      |
      v
+----------------------------+
| Internal/External Services |
| + Ingress-Nginx (optional) |
+----------------------------+
      |
      v
+----------------------------+
| Cluster Setup Job          |
| Initializes HA cluster     |
| registration               |
+----------------------------+
```

### Memgraph Lab Mode

```
Browser/User
      |
      v
+----------------------------+
| K8s Service (port 3000)    |
+----------------------------+
      |
      v
+----------------------------+
| Deployment (1+ replicas)   |
| Memgraph Lab Web UI        |
| Optional: HPA, Ingress     |
+----------------------------+
```

## Component Relationships

- **Memgraph standalone** is the base deployment unit: a single StatefulSet with persistent storage, service exposure, and optional monitoring.
- **Memgraph HA** builds on the same image but adds a coordination layer via coordinator pods that manage data instance replication and failover.
- **Memgraph Lab** is a separate stateless web application that connects to any Memgraph instance via the Bolt protocol (port 7687).
- **Prometheus exporter** is an optional sidecar deployment for both standalone and HA modes that exposes Memgraph metrics for scraping.

## Service Boundaries

| Service | Port | Protocol | Description |
| --- | --- | --- | --- |
| Bolt | 7687 | TCP | Primary database protocol for Cypher queries |
| WebSocket Monitoring | 7444 | TCP | Real-time monitoring via WebSocket |
| HTTP Monitoring | 9091 | TCP | Prometheus metrics endpoint |
| Lab Web UI | 3000 | TCP | Memgraph Lab dashboard |

## Security Boundaries

- Pods run as non-root with security contexts (`runAsUser: 101`, `runAsGroup: 103`)
- Seccomp profile set to `RuntimeDefault`
- Capabilities are dropped: `ALL`
- Init containers requiring privileged mode run only when explicitly enabled (sysctl, core dumps)
- Secrets can be injected as environment variables for authentication
