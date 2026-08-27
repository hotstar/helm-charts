---
title: Memgraph Helm Charts Overview
last_reviewed: 2026-08-27
tags: [helm, memgraph, kubernetes, overview]
folder: overview
sources:
  - code:README.md
  - code:charts/memgraph/Chart.yaml
  - code:charts/memgraph-high-availability/Chart.yaml
  - code:charts/memgraph-lab/Chart.yaml
---

# Memgraph Helm Charts Overview

This repository provides Helm charts for deploying **Memgraph**, an open-source in-memory graph database, on Kubernetes.

## Repository Purpose

The repo serves as the official Helm chart repository for the Memgraph graph database ecosystem. It publishes three Helm charts to Artifact Hub and the Memgraph Helm repository at `https://memgraph.github.io/helm-charts`.

## Top-Level Layout

| Path | Purpose |
| --- | --- |
| `charts/memgraph/` | Standalone Memgraph database deployment (StatefulSet, PVC, Service) |
| `charts/memgraph-high-availability/` | HA Memgraph cluster with coordinators and data instances (Enterprise) |
| `charts/memgraph-lab/` | Memgraph Lab visualization tool deployment |
| `docker-compose/` | Local Docker Compose setup for HA cluster testing |
| `scripts/` | Utility scripts for EKS, AKS, GKE, debugging, and management |
| `tutorials/` | Platform-specific deployment guides (AWS, Azure/GCP linked to HA chart docs) |
| `index.yaml` | Helm repository index for chart discovery |
| `lintconf.yaml` | YAML linting configuration |

## What the Project Does

This repository enables users to:
- Deploy Memgraph standalone on Kubernetes for graph database workloads
- Deploy Memgraph Lab for visual graph data exploration
- Deploy a high-availability Memgraph cluster with two data instances and three coordinators for enterprise use cases
- Configure storage, networking, monitoring, and security via Helm values
- Deploy on multiple cloud platforms (AWS EKS, Azure AKS, GCP GKE)

## Chart Versions

| Chart | Current Version | App Version |
| --- | --- | --- |
| memgraph | 0.2.16 | 3.8.1 |
| memgraph-high-availability | 0.2.16 | 3.8.1 |
| memgraph-lab | 0.1.14 | 3.8.0 |

## Ownership

- Maintainer: Memgraph (tech@memgraph.com)
- License: Apache 2.0
- Homepage: https://memgraph.com/
