---
title: Branching and release conventions
last_reviewed: 2026-08-27
tags: [readiness-placeholder, branching-release-conventions]
folder: engineering
sources:
  - repo-doc:CONTRIBUTING.md
  - code:Chart.yaml
agent_routing:
  code_change_relevance: conditional
  task_intents: [repo-onboarding]
  applies_to_paths: []
  applies_to_symbols: []
---

# Branching and release conventions

> Readiness page: generated from repo evidence for `branching-release-conventions` and still needs human review.

## Branching

- All bug fixes and new features should be applied to the `main` branch.
- No specific branch naming conventions are documented.

## Pull Requests

- A review by two code owners is required for PRs to be merged.
- Tests need to pass remotely before merging.
- Commits should be atomic (one feature per commit).

## Versioning

Chart versions follow semantic versioning as declared in each chart's `Chart.yaml`:
- Memgraph standalone: `version: 0.2.16`, `appVersion: 3.8.1`
- Charts are published as `.tgz` archives to the Helm repository

## Suggested Content

- Document the release process for publishing new chart versions.
- Add Helm repository index update procedures.
- Document changelog expectations.
- Add deployment gate and rollback procedures.
- Add versioning policy for chart and app versions.
