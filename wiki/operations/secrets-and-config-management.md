---
title: Secrets and config management rules
last_reviewed: 2026-08-27
tags: [readiness-placeholder, secrets-config-management]
folder: operations
sources:
  - code:charts/memgraph/values.yaml
  - code:charts/memgraph-high-availability/values.yaml
agent_routing:
  code_change_relevance: conditional
  task_intents: [operations-change]
  applies_to_paths: []
  applies_to_symbols: []
---

# Secrets and config management rules

> Readiness page: generated from repo evidence for `secrets-config-management` and still needs human review.

## Supported Secrets Configuration

The Memgraph standalone chart supports Kubernetes secrets for authentication:
- `secrets.enabled` — enable use of Kubernetes secrets for Memgraph credentials
- `secrets.name` — name of the Kubernetes secret containing Memgraph credentials
- `secrets.userKey` — key in the Kubernetes secret for the Memgraph user (`MEMGRAPH_USER` env)
- `secrets.passwordKey` — key in the Kubernetes secret for the Memgraph password (`MEMGRAPH_PASSWORD` env)

When enabled, the secrets are injected as environment variables in the Memgraph container.

## Enterprise License Configuration

- `memgraphEnterpriseLicense` and `memgraphOrganizationName` are set as environment variables (`MEMGRAPH_ENTERPRISE_LICENSE`, `MEMGRAPH_ORGANIZATION_NAME`)
- These values are typically passed at install time via `--set` flags

## Secret Creation

```bash
kubectl create secret generic memgraph-secrets --from-literal=USER=myuser --from-literal=PASSWORD=mypassword
```

## Suggested Content

- Document secret rotation procedures.
- Add guidance on managing secrets in CI/CD pipelines.
- Document recommended RBAC configurations for secret access.
- Add security best practices for production deployments.
- Document how to mount TLS certificates for Bolt protocol.
