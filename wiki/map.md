# Wiki Map

## Understand the system

- [Repo Overview](overview/repo-overview.md) — What this repo contains, chart versions, and ownership.
- [Module Structure](architecture/module-structure.md) — How the three Helm charts are organized.
- [System Architecture](architecture/system-architecture.md) — Component relationships in standalone, HA, and Lab modes.
- [Domain Concepts](domains/domain-concepts.md) — Glossary of relevant technical and product terms.
- [Dependencies](architecture/dependencies.md) — External images, K8s requirements, and cloud provider needs.

## Change behavior

- [Helm Chart Values API](api/helm-chart-values-api.md) — Configuration surfaces for all charts.
- [Configuration](engineering/configuration.md) — Environment variables, feature flags, and config files.
- [Code and Naming Conventions](engineering/code-and-naming-conventions.md) — Contribution guidelines and chart structure conventions.
- [Data Models](data/data-models.md) — Storage model, persistence, and snapshot configuration.
- [Data Flow](data/data-flow.md) — Query, metrics, replication, and secret flow within deployments.

## Operate in production

- [IaC Info](operations/iac-info.md) — Kubernetes resources, cloud infrastructure, and Docker Compose.
- [Secrets and Config Management](operations/secrets-and-config-management.md) — Secrets, enterprise license, and auth management.
- [Production Context](operations/production-context.md) — Human-owned placeholder for production runtime constraints.
- [Build, Test, and Deploy](engineering/build-test-deploy.md) — Deployment commands, cloud-specific scripts, and CI/CD workflow.

## Onboard a new engineer

- [How to Set Up the Service](engineering/how-to-set-up-the-service.md) — Prerequisites, Helm setup, and installation commands.
- [How to Run Tests](engineering/how-to-run-tests.md) — Connection testing and contribution test requirements.
- [Branching and Release Conventions](engineering/branching-and-release-conventions.md) — Branch strategy, PR process, and versioning.
- [Entry Points](engineering/how-to-set-up-a-local-testing-environment.md) — Local dev workflow and Docker Compose.
