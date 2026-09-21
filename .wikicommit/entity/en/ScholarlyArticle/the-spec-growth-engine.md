---
title: "The Spec Growth Engine: Spec-Anchored, Code-Coupled, Drift-Enforced Architecture for AI-Assisted Software Development"
type: "schema:ScholarlyArticle"
lang: en
tags: [spec-driven-development, agents, context-engineering, governance]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.27045'
    hash: sha256:9004fd8330acfa64f27d8cc588f1234dd91b29303e4ee479b537bbdebca481f6
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Proposes the Spec Growth Engine, a framework that scopes an AI coding agent's context to an ownership path through a machine-readable spec graph and makes divergence between specification and code a blocking merge error rather than a matter of discipline."
  author: "Hartwig Grabowski"
  datePublished: "2026-06-25"
---

This paper argues that AI coding agents accelerate implementation while introducing two structural
failure modes it holds existing spec-driven approaches do not fully solve. The first is context
explosion: without scoping, giving an agent everything relevant means giving it the whole repository,
which the author says causes it to conflate concerns from unrelated modules and produce global fixes
touching boundaries it was not asked to change. The second is silent spec-code drift: developers
update the code and defer the spec update permanently, the tests still pass, and nothing flags the
divergence, so that a future agent run is guided by a stale specification. Of drift specifically the
paper stresses that the observation is not new — it points to earlier work on reflexion models and on
architectural erosion — but argues the cost is, because an agent generating several hundred lines per
minute from a stale spec accumulates damage far faster than traditional development.

The framework proposed in response, [[DefinedTerm/spec-growth-engine]], is positioned as a deliberately
lean middle ground between spec-first approaches, which generate full specifications before any code,
and spec-as-source systems, which generate code from specifications and which the author says
introduce nondeterminism and a fragile single point of truth that teams reject in practice. The paper
describes the engine as five interlocking components — a spec graph, a context assembler, a drift
validator, governance gates, and a capability registry providing a horizontal reuse axis — operated by
four actors with distinct authority, and mutated through a fixed set of growth rules. Its concluding
summary counts the vertical-slice growth protocol among the mechanisms in place of the registry.

The paper presents the design as a synthesis rather than a new paradigm, mapping each mechanism to an
established origin — information hiding for the contract/design split, the C4 model for its zoom
levels, architecture decision records, the Walking Skeleton and tracer bullet patterns for vertical
slices, the spiral model for hardest-first ordering, reflexion models for drift validation, and
fitness functions for automated checks — and claims the contribution is the integration layer: a
single framework enforcing all these properties at once through machine-readable artefacts and
blocking gates, at an overhead low enough for daily use.

## Key Points

- Argues that the root cause of context explosion is architectural rather than a model limitation:
  without a boundary saying what an agent working on one component is allowed to know, a developer
  must either give everything, which is expensive and noisy, or guess what is relevant, which is
  fragile and inconsistent.
- Separates a practitioner heuristic from the evidence behind it. The paper reports a commonly quoted
  rule of thumb about becoming cautious once a context window passes roughly 40% fill, states plainly
  that this is a rule of thumb from coding-agent practice rather than a proven threshold whose exact
  point depends on model and task, and holds that the underlying degradation is nonetheless well
  supported. It summarizes the takeaway as directional rather than numerical: less, well-chosen
  context beats more.
- Proposes a two-layer growth rule intended to prevent two opposite failures. Layer 1 fixes root
  invariants and key container boundaries — persistence, security, external integrations, error
  taxonomy — before any feature, deliberately not just-in-time; Layer 2 grows everything else as
  hardest-first vertical slices. The author argues breadth-first ordering hides hard problems in stubs
  until the end, while pure agile with no floor lets a needed boundary never appear because no feature
  happened to force it.
- Defines a frontier stub as a position plus a piece of governance rather than a kind of
  implementation: technically an ordinary placeholder, it counts as a frontier stub only because it
  sits off the current slice's active path and is tracked as an explicit exception naming its successor
  slice, so it cannot be mistaken for finished work. The same artefact on the active path would be a
  forbidden fake.
- Applies information hiding to agent context: the bundle an agent receives is the root invariants plus
  the contracts along the ownership path plus the node's own full spec, its own code, and the contracts
  of its declared dependencies one hop only — explicitly excluding sibling components, dependency
  designs and code, transitive dependencies, and ad-hoc search results. The assembler determines what
  the agent reads; the agent does not search freely.
- Makes spec-code alignment a structural property rather than a discipline: the engine derives an
  intent graph from the spec files and an evidence graph from static code analysis, and blocks a merge
  outright on orphan code, undeclared dependencies, dependencies bypassing a contract, or a missing
  dependency contract, while reporting weaker signals as non-blocking warnings.
- Ties review overhead to blast radius through three gate levels — human approval required, agent
  proceeds with asynchronous review, and no human at all — on the principle that changes to the
  outward surface are hard to reverse while changes to internal design are local and reversible.
- Separates authority between four actors, with the engine deterministic and authoring no intent,
  planner and coding agents authoring intent but subject to gates, and only a human architect approving
  changes to the outward surface. The author presents this separation as what makes an agent updating
  the spec in the same commit safe.

## Notes

The paper is a design proposal rather than an evaluated system. It contains no experiment, benchmark
or user study; its worked example traces a small e-commerce checkout through the machinery to
illustrate the mechanisms rather than to measure them. The author states that the Spec Growth Engine
is maintained as an internal design-document set, that a public release is planned, and that the
documents are available from the author on request.

Two limitations are stated. The design requires a static dependency graph derivable from source files,
so highly dynamic systems — runtime dependency injection, plugin architectures — need late-bound
dependencies annotated explicitly. And the governance gate overhead is described as real for
fast-moving teams, mitigated but not eliminated by the middle gate level.

The author also positions the engine against the software engineering body of knowledge, mapping the
spec graph to the architecture and design areas, drift validation to testing and quality, the
governance model to engineering management, and the vertical slice protocol to process, and describes
that body of knowledge as the background frame against which the engine's positioning can be checked.
