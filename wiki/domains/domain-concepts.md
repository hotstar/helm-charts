---
title: Domain Concepts
last_reviewed: 2026-08-27
tags: [domain, glossary, memgraph, graph-database]
folder: domains
sources:
  - code:README.md
  - code:charts/memgraph/Chart.yaml
  - code:charts/memgraph-high-availability/Chart.yaml
  - code:charts/memgraph/memgraph.conf
---

# Domain Concepts

## Memgraph

An open-source, in-memory graph database that supports the Cypher query language and provides ACID-compliant transactions. Data is stored in a property graph model (vertices, edges, properties).

## Bolt Protocol

The binary protocol used by Memgraph for client communication. It operates on port 7687 and is the primary interface for applications, mgconsole, and Memgraph Lab to interact with the database.

## Cypher

The graph query language used by Memgraph. It is the same query language used by Neo4j and allows declarative pattern matching on graph structures.

## Helm Chart

A package of pre-configured Kubernetes resources that define how an application should be deployed. This repository publishes three charts.

## StatefulSet

A Kubernetes workload resource used for stateful applications like Memgraph. It provides stable network identities and persistent storage through PVC templates, making it suitable for database deployments.

## PVC (Persistent Volume Claim)

A request for storage in Kubernetes. Memgraph uses PVCs for data storage, logs, and optional user data and core dumps. The default reclaim policy is `Retain`.

## Standalone Mode

A single Memgraph instance deployment with one replica. Suitable for development, testing, and non-critical workloads. No replication or automatic failover.

## High Availability (HA) Mode

Enterprise feature providing a Memgraph cluster with multiple data instances and coordinators. Uses raft-based consensus for cluster management. Provides failover and read scalability.

## Coordinator

In HA mode, coordinator instances manage cluster membership, route client queries to the appropriate data instance, and maintain consensus using the Raft protocol.

## Data Instance

In HA mode, data instances store and serve graph data. One instance acts as the primary for writes, while others serve as replicas for reads.

## mgconsole

The command-line tool for interacting with Memgraph via the Bolt protocol.

## Memgraph Lab

A web-based visual interface for exploring Memgraph databases, running Cypher queries, and visualizing graph data.

## Prometheus Exporter

A sidecar deployment that exposes Memgraph's internal metrics in Prometheus format, enabling monitoring and alerting via the Prometheus ecosystem.

## SysctlInitContainer

An init container that sets `vm.max_map_count` to 262144, required for Memgraph's memory-mapped file operations under high memory loads.

## Core Dump Uploader

An optional sidecar container (in HA mode) that watches for core dump files and uploads them to an S3 bucket for debugging.
