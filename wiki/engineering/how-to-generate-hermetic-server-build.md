---
title: How to generate hermetic server/build
last_reviewed: 2026-08-27
tags: [readiness-placeholder, hermetic-build]
folder: engineering
sources:
  - repo-doc:README.md
  - code:.github/
agent_routing:
  code_change_relevance: conditional
  task_intents: [repo-onboarding]
  applies_to_paths: []
  applies_to_symbols: []
---

# How to generate hermetic server/build

> Readiness page: generated from repo evidence for `hermetic-build` and still needs human review.

## Available Build Artifacts

This repository publishes Helm chart packages (`.tgz` archives) to the Memgraph Helm chart repository at `https://memgraph.github.io/helm-charts`.

The chart index is maintained in `index.yaml` at the repository root.

## Suggested Content

- Document the chart packaging process (e.g., `helm package` commands).
- Document how to sign and verify chart packages.
- Add CI/CD release pipeline documentation.
- Document versioning strategy for chart releases.
- Add instructions for building and testing charts locally before release.
