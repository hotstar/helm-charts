---
title: Configuration
last_reviewed: 2026-08-27
tags: [engineering, configuration, env-vars, feature-flags]
folder: engineering
sources:
  - code:charts/memgraph/values.yaml
  - code:charts/memgraph/memgraph.conf
  - code:charts/memgraph-high-availability/values.yaml
  - code:charts/memgraph-lab/values.yaml
---

# Configuration

## Environment Variables

### Memgraph Container
| Variable | Source | Description |
| --- | --- | --- |
| `MEMGRAPH_USER` | K8s secret (`secrets.userKey`) | Memgraph username for authentication |
| `MEMGRAPH_PASSWORD` | K8s secret (`secrets.passwordKey`) | Memgraph password |
| `MEMGRAPH_ENTERPRISE_LICENSE` | `values.memgraphEnterpriseLicense` | Enterprise license key |
| `MEMGRAPH_ORGANIZATION_NAME` | `values.memgraphOrganizationName` | Organization name for license |

### Prometheus Exporter
| Variable | Value | Description |
| --- | --- | --- |
| `DEPLOYMENT_TYPE` | `standalone` | Mode identifier |
| `CONFIG_FILE` | `/etc/mg-exporter/standalone_config.yaml` | Exporter configuration path |

### Core Dump Uploader (HA mode)
| Variable | Source | Description |
| --- | --- | --- |
| `WATCH_DIR` | Core dump PVC mount path | Directory to watch for core dumps |
| `S3_BUCKET` | `values.coreDumpUploader.s3BucketName` | S3 bucket for uploads |
| `S3_PREFIX` | `values.coreDumpUploader.s3Prefix` | S3 key prefix |
| `AWS_REGION` | `values.coreDumpUploader.awsRegion` | AWS region |
| `POLL_INTERVAL` | `values.coreDumpUploader.pollIntervalSeconds` | Watch interval in seconds |

### Memgraph Lab
| Variable | Description |
| --- | --- |
| `QUICK_CONNECT_MG_HOST` | Memgraph host for quick connect |
| `QUICK_CONNECT_MG_PORT` | Memgraph port (default: 7687) |
| `BASE_PATH` | Base URL path |

## Feature Flags

| Feature | Config Key | Default | Description |
| --- | --- | --- | --- |
| Prometheus monitoring | `prometheus.enabled` | `false` | Deploy Prometheus exporter |
| LoadBalancer service | `service.loadBalancer.enabled` | `false` | External cluster access |
| Secrets-based auth | `secrets.enabled` | `false` | Use K8s secrets for auth |
| HA mode | N/A (separate chart) | N/A | Deploy HA cluster |
| Core dumps PVC | `persistentVolumeClaim.createCoreDumpsClaim` | `false` | PVC for core dumps |
| User claim PVC | `persistentVolumeClaim.createUserClaim` | `false` | PVC for user files |
| Sysctl init | `sysctlInitContainer.enabled` | `true` | Set kernel params |

## Config Files

### Memgraph Configuration (`memgraph.conf`)
Located at `charts/memgraph/memgraph.conf`, this file provides the default Memgraph database configuration with documented settings for:
- **Audit**: Audit logging enable/disable
- **Auth**: Authentication module configuration
- **Bolt**: Bolt server address, port, TLS certificates
- **Log**: Log file path and level
- **Memory**: Memory limits (default: 0 = auto)
- **Metrics**: Metrics endpoint configuration
- **Query**: Query planner, execution timeout, plan caching
- **Storage**: Snapshot settings, WAL, recovery, GC
- **Stream**: Kafka/Pulsar stream configuration
- **Replication**: Replica check frequency

### Helm Values Files
- `values.yaml` per chart — default configuration for all parameters
- `charts/memgraph-high-availability/aks/values-aks.yaml` — AKS-specific overrides

## Init Container Configuration

The sysctl init container is a critical configuration mechanism:
- Sets `vm.max_map_count = 262144`
- Required for high memory loads in Memgraph
- Can be disabled via `sysctlInitContainer.enabled: false`
