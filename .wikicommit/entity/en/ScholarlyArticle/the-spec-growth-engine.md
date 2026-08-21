---
title: "The Spec Growth Engine: Spec-Anchored, Code-Coupled, Drift-Enforced Architecture for AI-Assisted Software Development"
type: "schema:ScholarlyArticle"
lang: en
tags: [spec-driven-development, architecture, context-engineering, governance]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.27045'
    hash: sha256:9004fd8330acfa64f27d8cc588f1234dd91b29303e4ee479b537bbdebca481f6
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A framework proposal addressing two failure modes of AI-assisted development — context explosion and silent spec-code drift — through a machine-readable spec graph, an ownership-path context assembler, a hardest-first vertical-slice growth protocol, and a drift gate that blocks merges."
  author: ["Hartwig Grabowski"]
  datePublished: "2026-06-26"
  abstract: "Presents the Spec Growth Engine, a framework combining a spec graph with explicit contract/design separation, a Spine context assembler scoping agent context to an ownership path, a hardest-first vertical-slice growth protocol, and a drift gate making spec-code divergence a blocking merge condition."
  keywords: ["specification-driven development", "context engineering", "software architecture", "AI coding agents", "architectural drift", "information hiding"]
  citation: ""
---

This paper, by Hartwig Grabowski of Hochschule Offenburg, proposes a framework it calls the **Spec Growth Engine**. Its stated premise is that AI coding agents accelerate implementation while introducing two structural failure modes that existing spec-driven approaches do not fully solve: *context explosion*, where the agent must reason over an entire repository at once and output quality degrades as the context window fills; and *silent spec-code drift*, where code evolves, the specification does not, and the divergence stays invisible until repair is costly.

Its positioning is deliberately between two extremes it says both fail. Spec-first frameworks generate full specifications before any code, at the cost of upfront overhead and the risk of specifying the wrong thing. Spec-as-source systems generate code from specifications, introducing nondeterminism and a fragile single point of truth that the paper says teams consistently reject in practice. The engine is instead *spec-anchored* (every node has a spec), *code-coupled* (code and spec evolve in the same commit), and *drift-enforced* (divergence is a blocking merge error rather than a discipline problem).

The paper is explicit that it is not proposing a new paradigm: it presents itself as a lean, machine-enforced synthesis of established techniques — Parnas information hiding, the C4 model, Architecture Decision Records, the Walking Skeleton, Reflexion Models, and fitness functions — with the integration layer as the contribution, at an overhead low enough for daily use with agents and without the weight of frameworks such as RUP or MDA. It is a design proposal; no empirical evaluation of the engine is reported.

## Key Contributions

**A spec graph.** Every architectural entity is a node materialised as exactly one `SPEC.md` file, organised at the four C4 zoom levels — system, container, component, code. Each node carries two orthogonal views: a **contract** (outward — public interfaces, invariants, types, error behaviour, acceptance criteria, constraints) that neighbours may read, and a **design** (inward — internal approach, implementation, internal relations, children and code ownership) visible only to the node's implementer and its parent. Two edge types exist: ownership edges forming a tree, where a parent's contract is the sum of its children's contracts; and dependency edges forming a DAG, where a node may use another's contract but never its design or code.

**The [[DefinedTerm/spine]]**, a deterministic context assembler that scopes what an agent reads to the ownership path from graph root to working node, plus root invariants and the one-hop contracts of declared dependencies.

**A two-layer growth rule.** Layer 1 — root invariants and key container boundaries such as persistence, security, external integrations and the error taxonomy — is specified before any feature and is explicitly *not* just-in-time, forming a floor below which architecture cannot silently erode. Layer 2 — everything else — grows as functional vertical slices ordered hardest-first, with slice #1 a tracer bullet through the riskiest integration. The rule is designed to block two pathological orderings the paper says both fail: breadth-first with hard problems hidden in stubs until the end, and pure agile with no floor, where a needed boundary never appears because no feature happened to force it.

**A frontier stub discipline.** Fakes are permitted only at the frontier — standing in for a dependency a later slice will build — never on the current slice's active path. What makes a placeholder a frontier stub is position plus governance: it sits off the active path, and it is tracked as an explicit exception naming its successor slice, keeping the node at status `specd` so it can never be mistaken for done. Its purpose is to expose the contract the current node depends on, since a node may depend only on a contract, never on internal code.

**A drift gate**, described under [[DefinedTerm/spec-code-drift]], comparing an Intent Graph derived from the spec files against an Evidence Graph derived from static code analysis, and blocking merges where they disagree.

**A four-actor authority model.** A Human Architect holds decision rights over boundaries, public contracts and root invariants, approves consequential changes and grants exceptions. A Planner Agent proposes decomposition and drafts contracts, acceptance criteria and design, authoring intent subject to a gate. A Coding Agent implements one node inside its context bundle, maintains that node's design, and declares its observed dependencies. The Engine is deterministic — deriving the index, validating drift, enforcing gates and proposing diffs — and authors no intent. The paper names the critical line as the one between Engine and agents: the Engine never invents architecture, and only the Human Architect may approve changes to the outward surface.

## Notes

The paper is careful to separate practitioner heuristic from research evidence on context degradation. It records that practitioners call the high-fill regime the "Dumb Zone," with an often-quoted rule of thumb to become cautious past roughly 40% fill and not treat the last ~60% as a working zone — and states plainly that this is a rule of thumb from coding-agent practice, not a proven threshold, with the exact point depending on model and task. The underlying effect it treats as well supported, citing research that models use long contexts unevenly and retrieve worst from the middle, that quality falls consistently as input grows, and that on long-context coding specifically a strong model dropped from 29% to 3% on a software-engineering benchmark as the window grew from 32K to 256K tokens. Its stated takeaway is directional rather than numerical: less, well-chosen context beats more.

On drift it makes a similar distinction between the observation and its stakes. It notes that the pattern is not new — citing Reflexion Model work and the coinage of "architectural erosion" in the same era — and locates what is new in the cost: when an agent generates several hundred lines per minute guided by a stale spec, the damage accumulates far faster than in traditional development.

Two artefacts carry the whole written architecture in this design. A single transversal `ARCHITECTURE.md` holds the cross-cutting Layer-1 invariants, principles, ADRs, security policies and naming conventions; it is not a node, has no owner, and is prepended automatically to every context bundle. Per-node `SPEC.md` files hold the Layer-2 feature layer. Everything else — the index, the dependency graph, the drift report — is derived rather than hand-authored.
