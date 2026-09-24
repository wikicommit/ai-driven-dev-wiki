---
title: "Specification-Driven DevOps for Multi-Service Environments"
type: "schema:ScholarlyArticle"
lang: en
tags: [spec-driven, devops, infrastructure-as-code, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.25141'
    hash: sha256:bce113686ce4ff5295a6c96d9b908892cec698298ae9b35c50deee004fce5172
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An EPAM Systems study of whether a frontier LLM can generate Dockerfiles and Docker Compose configurations for multi-service applications from repository contents alone, which separates functional correctness from deployment-intent fidelity and derives a minimal explicit deployment specification for what repositories cannot convey."
  author: ["Oleg Grynets", "Kyrylo Fursov", "Vasyl Lyashkevych", "Volodymyr Veres"]
  abstract: "Three heterogeneous multi-service repositories were used to test whether GPT Codex 5.3, via GitHub Copilot, could generate Dockerfiles and Docker Compose configurations without access to developer-authored deployment artifacts, evaluated with deterministic end-to-end HTTP oracles and manual structural comparison. All three environments became operational, one after a Rust base-image update, and the model reconstructed service topology, ports, dependencies, hostnames, a background worker, hidden proxy configuration and a file-based secrets mechanism; it consistently omitted network segmentation, multi-stage builds, dependency-layer caching, live-reload volumes, production frontend serving, restrictive backend-port policies and cross-platform build logic. From these observations the study formalises the distinction between functional correctness and deployment-intent fidelity and derives a minimal explicit deployment specification."
  keywords: ["large language models", "Specification-Driven DevOps", "Docker Compose", "Dockerfile generation", "multi-service environments", "deployment intent", "functional oracle", "Infrastructure as Code"]
---

This paper, by four authors at EPAM Systems, asks whether the data available in an application's
repository is sufficient for an LLM to deploy a working multi-service environment, and what it
cannot convey. It observes that prior work on automated environment creation mostly targets a single
test-oriented container, and that LLM-based Infrastructure as Code generation usually starts from an
expert-written description of the desired infrastructure; here the model instead has to recover the
deployment from source code, manifests and configuration, with the repository's own Dockerfiles and
Compose files withheld.

The experiment used GPT Codex 5.3 through GitHub Copilot on an Apple M1 Pro (ARM64) host and three
public repositories from Docker's sample collections: `example-voting-app` (Python, Node.js and
.NET services with Redis and PostgreSQL), `react-rust-postgres` (React, Rust/Actix Web and
PostgreSQL) and `react-java-mysql` (React, Java Spring Boot and a MariaDB/MySQL database). Each
generated environment was judged by a deterministic end-to-end HTTP request through the whole service
pipeline — rather than by syntax, image builds or textual similarity — and then compared manually with
the developer-authored artifacts.

## Key Points

- All three generated environments became functionally operational: two on the first build and the
  Rust one after its base image was changed from Rust 1.85 to 1.88 to satisfy the current Actix Web
  dependency, giving a first-build success rate of 2/3 and a final rate of 3/3.
- The model correctly reconstructed language ecosystems, application ports, infrastructure services,
  hostnames and `depends_on` relationships in all three cases, identified a .NET background worker
  with no HTTP endpoint, discovered a frontend proxy configured in `setupProxy.js`, and inferred a
  Docker secrets mechanism from a bare `db/password.txt` file.
- Where credentials existed only in the withheld Compose file, the model invented alternative values
  but propagated them consistently, and the environment still passed; the authors conclude that for
  underdetermined values, internal consistency may matter more than reproducing the developer's
  literal values.
- It consistently omitted deployment intent: network segmentation (0/3, a flat network every time),
  multi-stage Dockerfiles, dependency-layer caching and live-reload mounts (0/3 each), production
  frontend serving through Nginx (0/2), restrictive backend-port exposure (0/2, backend ports were
  published to the host) and cross-platform build logic (0/3). The authors call this gap between
  required deployment knowledge and what a repository reveals the signal gap.
- The authors classify DevOps knowledge as directly observable, derivable, underdetermined or
  intent-only, and argue that observable and derivable knowledge was generally reconstructable while
  underdetermined and intent-only knowledge needs explicit specification or controlled defaults.
- On that basis they propose [[DefinedTerm/specification-driven-devops]], in which repository
  evidence supplies what is observable and a minimal explicit deployment specification supplies the
  rest, and sketch its fields, conflict-resolution principles, validation rules and a traceability
  model. This specification is analytically derived and was not tested by regeneration.

## Notes

The paper situates itself between LLM-based Dockerfile and environment synthesis work, IaC
generation benchmarks, and specification-driven approaches such as code-text-code re-engineering and
architecture metamodels, several of which are earlier work by the same authors. The authors present
it as an exploratory feasibility experiment and list its limits: three relatively simple, publicly
available repositories the model may have encountered in training; a single model and a single
generation attempt per repository with an incompletely documented interaction record; one HTTP oracle
per repository with no security, performance or failure testing; manual structural comparison by the
authors without a formal rubric; a manual rather than LLM-driven fix for the Rust version; and no
experimental validation of the proposed specification.
