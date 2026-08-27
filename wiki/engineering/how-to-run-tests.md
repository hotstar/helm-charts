---
title: How to run tests
last_reviewed: 2026-08-27
tags: [readiness-placeholder, test-commands]
folder: engineering
sources:
  - code:charts/memgraph/templates/tests/test-connection.yaml
  - repo-doc:CONTRIBUTING.md
agent_routing:
  code_change_relevance: conditional
  task_intents: [repo-onboarding]
  applies_to_paths: []
  applies_to_symbols: []
---

# How to run tests

> Readiness page: generated from repo evidence for `test-commands` and still needs human review.

## Available Test Resources

The repository includes a Helm test template for connection testing:
- `charts/memgraph/templates/tests/test-connection.yaml` — tests pod connectivity via the Bolt port.

Contributions require tests to pass remotely before a pull request can be merged. A review by two code owners is required.

## Suggested Content

- Add explicit chart linting and testing commands (e.g., `helm lint`, `helm template --debug`).
- Document how to run `helm test` for chart connection verification.
- Add unit testing instructions for template rendering.
- Document required test dependencies (e.g., Helm, Kubernetes cluster, kind or Minikube).
- Add CI workflow testing documentation.
