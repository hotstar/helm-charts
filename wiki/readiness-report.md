# LLM-Wiki Readiness Report

Overall score: 34/100 - Not ready

## Summary

This repo provides well-structured Helm charts for deploying Memgraph on Kubernetes. The README and per-chart documentation offer clear setup instructions and configuration options. However, there is no dedicated documentation for local testing environments, test commands, production runtime context, customer context, build/release processes, or architectural decisions. While infrastructure-as-code documentation is strong (the repo itself is IaC), other readiness areas need human-authored content to become actionable.

## Topic Scores

| Topic | Score | Evidence | Gap |
| --- | ---: | --- | --- |
| How to set up the service | 9/12 | README.md, charts/*/README.md, wiki/engineering/how-to-set-up-the-service.md | Setup commands documented but not execution-verified (agentic mode); missing local service reset steps |
| How to set up an environment for local testing | 2.5/10 | docker-compose/docker-compose.yml | No dedicated local testing documentation; docker-compose exists but no guide for chart template testing |
| How to run tests | 3.5/14 | charts/memgraph/templates/tests/test-connection.yaml, CONTRIBUTING.md | Only connection test template exists; no lint/unit/e2e test commands documented |
| IaC info | 8/8 | README.md, charts/*/templates/, charts/*/values.yaml, wiki/operations/iac-info.md | Strong documentation; charts, templates, and cloud deployment guides present |
| Production context | 0/12 | None found | No production runtime context documented |
| Customer context | 0/10 | None found | No customer context documented |
| How to generate hermetic server/build | 2.5/10 | index.yaml | Chart index exists but no build/release pipeline documentation |
| Code and naming conventions | 4/8 | CONTRIBUTING.md, lintconf.yaml, .pre-commit-config.yaml | Some conventions documented, but no detailed chart or Helm naming guide |
| Secrets and config management rules | 5/10 | charts/memgraph/values.yaml, charts/memgraph-high-availability/values.yaml | Secrets configuration is documented in values.yaml; no rotation or best practices guide |
| Branching and release conventions | 4/8 | CONTRIBUTING.md, Chart.yaml | Basic branch/PR rules documented; no formal release process or changelog conventions |
| Edge cases decided outside code | 0/10 | None found | No edge case documentation |
| Known tradeoffs and rejected alternatives | 2.5/10 | README.md, charts/memgraph/values.yaml | Some tradeoffs documented inline (image tags, memory limits); no formal ADRs |

## Top Gaps

1. Add production runtime context documentation (hot paths, performance budgets, production service identity).
2. Add customer context documentation (customer journeys, callers, segments, business rules).
3. Add local testing environment setup guide and test commands documentation.
4. Add document build/release pipeline and chart publishing process.
5. Add ADRs and formal tradeoff documentation.

## Suggested Wiki Changes

| Priority | Wiki path | Exact change |
| --- | --- | --- |
| High | `wiki/operations/production-context.md` | Fill agent-critical constraints, production service identity, hot paths, change guardrails, validation pointers, and risky change patterns with production-owner reviewed facts. |
| High | `wiki/domains/customer-context.md` | Fill customer journeys, callers, segments, contracts, business rules, and impact sections with product-owner reviewed facts. |
| High | `wiki/engineering/how-to-set-up-a-local-testing-environment.md` | Document Docker Compose usage for local HA cluster, Minikube setup for chart testing, and verification steps. |
| High | `wiki/engineering/how-to-run-tests.md` | Add chart linting commands, `helm template --debug`, `helm test`, and CI workflow test documentation. |
| Medium | `wiki/engineering/how-to-generate-hermetic-server-build.md` | Document `helm package`, chart signing, and CI/CD release pipeline. |
| Medium | `wiki/engineering/branching-and-release-conventions.md` | Add formal release process, changelog conventions, and deployment gates. |
| Medium | `wiki/decisions/tradeoffs-and-rejected-alternatives.md` | Add formal ADR records for significant architectural decisions. |

## Repo Docs Migration

| Repo doc | Wiki target | Recommendation | Drift or conflict |
| --- | --- | --- | --- |
| `README.md` | `wiki/engineering/how-to-set-up-the-service.md`, `wiki/operations/iac-info.md` | Wiki pages populated from this doc; remove or deprecate the repo doc only after the wiki page is reviewed and accepted. | No conflict found. |
| `CONTRIBUTING.md` | `wiki/engineering/code-and-naming-conventions.md`, `wiki/engineering/branching-and-release-conventions.md` | Wiki pages populated from this doc; remove or deprecate after the wiki pages are accepted as canonical. | No conflict found. |
| `charts/memgraph/README.md` | `wiki/engineering/how-to-set-up-the-service.md` | Wiki page populated from this doc; remove or deprecate after the wiki is accepted as canonical. | Partial coverage: wiki page includes code-derived configuration details. |
| `charts/memgraph/values.yaml` | `wiki/operations/iac-info.md`, `wiki/operations/secrets-and-config-management.md`, `wiki/decisions/tradeoffs-and-rejected-alternatives.md` | Wiki pages populated from this config file; config file should remain as source of truth for values. | No conflict found. |

## Evidence Notes

- `README.md` and per-chart READMEs were counted as strong evidence for setup and IaC topics.
- `CONTRIBUTING.md` provided evidence for code conventions and branching/release topics.
- Chart `values.yaml` files were counted as moderate evidence for configuration and secrets topics.
- Secret-bearing files were detected but not read.
- No command execution verification was performed (agentic mode). Topics with `execution_required: true` had commands from documentation skipped and scores capped accordingly.
- No prior readiness report exists to archive (first run).
