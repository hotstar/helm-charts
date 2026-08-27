---
title: Code and naming conventions
last_reviewed: 2026-08-27
tags: [readiness-placeholder, code-and-naming-conventions]
folder: engineering
sources:
  - repo-doc:CONTRIBUTING.md
  - code:lintconf.yaml
  - code:.pre-commit-config.yaml
  - code:charts/
agent_routing:
  code_change_relevance: conditional
  task_intents: [repo-onboarding]
  applies_to_paths: []
  applies_to_symbols: []
---

# Code and naming conventions

> Readiness page: generated from repo evidence for `code-and-naming-conventions` and still needs human review.

## Contributing Guidelines

Contributions follow the standard fork-and-PR workflow. Two code owner reviews are required for merging. All commits should be atomic (one feature per commit). Bug fixes and new features should target the `main` branch.

## YAML Linting

The repository uses a YAML lint configuration at `lintconf.yaml` that enforces:
- Consistent indentation (spaces)
- Unix-style line endings
- Trailing spaces detection
- Comment formatting rules
- YAML key uniqueness enforcement

## Pre-commit Hooks

A `.pre-commit-config.yaml` file exists for automated pre-commit checks.

## Helm Chart Structure

Charts follow the standard Helm chart directory layout:
- `Chart.yaml` — chart metadata
- `values.yaml` — default configuration values
- `templates/` — Kubernetes resource templates
- `templates/tests/` — Helm test templates
- `README.md` — per-chart documentation

Additional directories for provider-specific configurations:
- `charts/memgraph-high-availability/aks/` — Azure AKS deployment files
- `charts/memgraph-high-availability/aws/` — AWS deployment files

## Suggested Content

- Add Helm chart naming conventions for releases, resources, and labels.
- Document template helper functions and naming patterns in `_helpers.tpl`.
- Add review checklist for chart contributions.
- Document expected PR title and commit message format.
