---
title: "Specification-Driven DevOps"
type: "schema:DefinedTerm"
lang: en
tags: [spec-driven, devops, infrastructure-as-code]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.25141'
    hash: sha256:bce113686ce4ff5295a6c96d9b908892cec698298ae9b35c50deee004fce5172
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An approach to LLM-based generation of deployment environments in which facts observable or derivable from an application's repository are inferred from it, while deployment decisions the repository cannot convey are supplied through a compact, explicit deployment specification."
---

Specification-Driven DevOps is an approach proposed in
[[ScholarlyArticle/specification-driven-devops-for-multi-service-environments]] that treats the
generation of a deployment environment as a managed transformation: directly observable deployment
facts are derived from repository artifacts, while DevOps decisions that are not observable or are
insufficiently defined are stated in a compact, explicit specification. The repository is therefore
not regarded as an exhaustive specification but as one information source in a hybrid model, in
which the environment is generated from the repository, a minimal explicit deployment specification,
external technological knowledge and the generative model. The authors describe it as closely linked
to specification-based development more broadly (see [[DefinedTerm/spec-driven-development]]).

## Usage

The motivation is the distinction the authors draw between functional correctness — whether a
generated environment builds, starts and runs its end-to-end pipeline — and deployment-intent
fidelity, the degree to which it reproduces the developer's architectural, security, workflow and
production decisions. In their experiment, an LLM generated working Dockerfiles and Docker Compose
configurations for three multi-service applications from repository contents alone, but consistently
omitted network segmentation, multi-stage builds, dependency-layer caching, live-reload mounts,
production frontend serving, restrictive port exposure and cross-platform build logic. They classify
DevOps knowledge as directly observable (ports, imports, connection strings), derivable (service
topology, proxy routes, worker roles), underdetermined (credentials, compatible image versions) or
intent-only (network trust boundaries, public versus internal services, build strategy, production
serving), and place the last two in the specification.

The specification is meant to be minimal: it should contain only what is absent from or
underdetermined by the repository, represents workflow, security, platform or production intent, and
must not be replaced by an arbitrary model default — repeating facts the source code already encodes
would create duplication and maintenance cost. The authors sketch it as a `deployment-spec.yml`
covering deployment context (environment mode and target platform), workflow (live reload, debug
ports), network policy (segmentation and public versus internal services), build strategy
(multi-stage builds, named targets, cross-platform arguments), secret mechanism, production serving
and infrastructure constraints. They propose that explicit policy override inferred defaults, that a
specified runtime version override a compatible inferred one, that explicit secret policy override
secret handling visible in the repository, and that a passing functional test not be treated as
security-policy compliance, and they add validation rules and a traceability model recording whether
each generated element came from the repository, the specification or an ungrounded default.

The approach positions itself between two extremes: repository-only generation, which is efficient
but may silently introduce unsafe or unsuitable defaults, and a complete hand-written deployment
specification, which duplicates information already in the source code.

## When It Applies

- Applies to generating deployment environments — Dockerfiles, Compose configurations, networks,
  volumes, secrets and port policies — for multi-service applications, where some deployment
  decisions have no reliable representation in the implementation.
- Assumes the repository carries enough evidence for the observable and derivable parts of the
  deployment, such as source code, dependency manifests, configuration files and auxiliary artifacts.
- Its proposers identify the risks it targets as repository-only generation silently filling intent
  gaps with defaults, and treating functional success as if it established security or production
  readiness.
- It is at the proposal stage: it was introduced in one exploratory study of three relatively simple
  public repositories, and its authors state that the specification was derived analytically from
  observed omissions and was not evaluated by regenerating environments with it, so the study
  establishes its structure but not its effectiveness.

## Related Terms

- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/executable-ssot]]
- [[DefinedTerm/semi-executable-artifact]]
