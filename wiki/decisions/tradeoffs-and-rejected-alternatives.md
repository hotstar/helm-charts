---
title: Known tradeoffs and rejected alternatives
last_reviewed: 2026-08-27
tags: [readiness-placeholder, tradeoffs-rejected-alternatives]
folder: decisions
sources:
  - repo-doc:README.md
  - code:charts/memgraph/values.yaml
agent_routing:
  code_change_relevance: conditional
  task_intents: [repo-onboarding]
  applies_to_paths: []
  applies_to_symbols: []
---

# Known tradeoffs and rejected alternatives

> Readiness page: generated from repo evidence for `tradeoffs-rejected-alternatives` and still needs human review.

## Documented Tradeoffs

### Image Tag Best Practices
The chart documentation explicitly warns against setting image tags to `latest` as it can trigger automatic upgrades on pod restarts. Charts should pin specific versions.

### Memory Configuration Warning
Setting Memgraph's `--memory-limit` flag to an amount less than the pod's allocated memory can trigger pod eviction and restarts. Memory limits should be carefully coordinated with container resource limits.

### Storage Configuration
- Default storage class configuration assumes Minikube; production deployments must configure appropriate storage classes for their cloud provider.
- Persistent Volume Claim reclaim policies affect whether data persists after Helm release deletion.

### Resource Limits
Resources are intentionally left empty by default so users can make conscious choices based on their deployment needs.

## Suggested Content

- Add ADR records for significant architectural decisions.
- Document why Helm charts were chosen over other deployment methods.
- Add comparisons with alternative Memgraph deployment options (Docker, binary).
- Document decisions around HA cluster architecture (2 data instances + 3 coordinators).
