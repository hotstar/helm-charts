---
title: Production context
last_reviewed: 2026-08-27
tags: [readiness-placeholder, production-context, agent-context]
folder: operations
sources:
  - repo-doc:README.md
  - code:charts/memgraph/values.yaml
agent_routing:
  code_change_relevance: conditional
  task_intents: [production-impact-change, operations-change]
  applies_to_paths: []
  applies_to_symbols: []
---

# Production context

> Readiness page: generated as a human-owned production-context placeholder and still needs human review.

## Agent-critical constraints

<!-- Add short constraints agents must honor before making or reviewing changes, such as p95 budget, no extra network call, no response-shape change, or required feature flag. -->

## Production service identity

<!-- Add deployable service name, prod aliases, owning team, pager/oncall, and cases where code/module names differ from prod names. -->

## Hot paths and performance budgets

<!-- Add latency targets, p50/p95/p99, QPS, timeout budgets, payload limits, cost-sensitive paths, and known bottlenecks. -->

## Runtime change guardrails

<!-- Add only the production constraints that directly change implementation, rollout, validation, or review choices, such as required feature flags, rollout shape, rollback expectations, or compatibility limits. Link to API, data, release, or runbook pages for details. -->

## Production validation pointers

<!-- Add the minimum checks an agent should know after a change, such as dashboard, metric, alert, trace, or log pointers. Link to canonical runbooks or SLO docs for full procedures. -->

## Known risky change patterns

<!-- Add concise patterns that commonly cause production regressions, such as fanout, blocking calls, cache-key changes, payload growth, or fragile dependency behavior. Link to incidents or decisions for details. -->

## Source References

<!-- Add source docs, runbooks, dashboards, incident reviews, or code/config evidence used to populate this page. -->

## Suggested Content

- Fill all TBD sections with production-owner reviewed facts.
- Add only constraints that should affect implementation, review, rollout, validation, or operational planning.
- Link to canonical architecture, API, data, release, runbook, SLO, incident, or observability pages instead of duplicating them here.
