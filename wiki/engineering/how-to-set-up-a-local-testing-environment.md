---
title: How to set up an environment for local testing
last_reviewed: 2026-08-27
tags: [readiness-placeholder, local-testing-environment]
folder: engineering
sources: []
agent_routing:
  code_change_relevance: conditional
  task_intents: [repo-onboarding]
  applies_to_paths: []
  applies_to_symbols: []
---

# How to set up an environment for local testing

> Readiness page: generated from repo evidence for `local-testing-environment` and still needs human review.

No dedicated local testing environment documentation was found in the repository. The repository provides Docker Compose files under `docker-compose/` for running a local HA Memgraph cluster, but no formal testing environment setup guide exists.

## Suggested Content

- Document how to use `docker-compose/docker-compose.yml` for local testing.
- Describe how to configure local-only Helm overrides for Minikube or kind clusters.
- Document mock services or dependencies needed for testing chart templates.
- Add instructions for seeding test data.
- Document verification steps before chart tests run.
