---
title: Helm Chart Values API
last_reviewed: 2026-08-27
tags: [api, helm, configuration, values, contracts]
folder: api
sources:
  - code:charts/memgraph/values.yaml
  - code:charts/memgraph-high-availability/values.yaml
  - code:charts/memgraph-lab/values.yaml
---

# Helm Chart Values API

The Helm chart values serve as the public configuration API for deploying Memgraph on Kubernetes. Key configuration categories are summarized below.

## Source Repository

Charts are sourced from the Memgraph Helm repository:
```
helm repo add memgraph https://memgraph.github.io/helm-charts
```

## Memgraph Standalone Configuration API

### Image Configuration
| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `image.repository` | string | `docker.io/memgraph/memgraph` | Docker image repository |
| `image.tag` | string | `""` (defaults to appVersion) | Specific image tag |
| `image.pullPolicy` | string | `IfNotPresent` | Image pull policy |

### Service Configuration
| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `service.type` | string | `ClusterIP` | K8s service type |
| `service.enableBolt` | bool | `true` | Enable Bolt protocol on port 7687 |
| `service.enableWebsocketMonitoring` | bool | `false` | Enable WebSocket monitoring on port 7444 |
| `service.enableHttpMonitoring` | bool | `false` | Enable HTTP monitoring on port 9091 |
| `service.loadBalancer.enabled` | bool | `false` | Create external LoadBalancer service |

### Storage Configuration
| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `persistentVolumeClaim.storageSize` | string | `10Gi` | Storage size for data |
| `persistentVolumeClaim.logStorageSize` | string | `1Gi` | Storage size for logs |
| `persistentVolumeClaim.storageClassName` | string | `""` | Storage class name |

### Enterprise Features
| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `memgraphEnterpriseLicense` | string | `""` | Enterprise license string |
| `memgraphOrganizationName` | string | `""` | Organization name for license |

### Authentication
| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `secrets.enabled` | bool | `false` | Enable K8s secrets for authentication |
| `secrets.name` | string | `memgraph-secrets` | Secret name |
| `secrets.userKey` | string | `USER` | Secret key for username |
| `secrets.passwordKey` | string | `PASSWORD` | Secret key for password |

### Monitoring
| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `prometheus.enabled` | bool | `false` | Deploy Prometheus exporter |
| `prometheus.memgraphExporter.port` | int | `9115` | Exporter port |
| `prometheus.serviceMonitor.enabled` | bool | `true` | Deploy ServiceMonitor |

## Memgraph Lab Configuration API

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `image.repository` | string | `docker.io/memgraph/lab` | Docker image |
| `service.port` | int | `3000` | Service port |
| `service.targetPort` | int | `3000` | Target port |
| `secrets.enabled` | bool | `false` | Enable secrets for env injection |

## Memgraph HA Configuration API

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `env.MEMGRAPH_ENTERPRISE_LICENSE` | string | `""` | Enterprise license |
| `env.MEMGRAPH_ORGANIZATION_NAME` | string | `""` | Organization name |
| `data` | array | `[]` | Data instance configurations |
| `coordinators` | array | `[]` | Coordinator configurations |
| `affinity` | object | `{}` | Node selection and anti-affinity policies |
