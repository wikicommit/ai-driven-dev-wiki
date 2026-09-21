---
title: "Spec Growth Engine"
type: "schema:DefinedTerm"
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
  description: "A framework for AI-assisted development built around a machine-readable spec graph, in which an agent's context is scoped to an ownership path through the graph and specification-code divergences of defined kinds block the merge."
---

The Spec Growth Engine is a framework for AI-assisted software development proposed in
[[ScholarlyArticle/the-spec-growth-engine]]. It is characterized by its author as spec-anchored,
meaning every architectural node carries a specification and that specification is kept a living
artefact rather than discarded after generation; code-coupled, meaning code and specification change in
the same commit; and drift-enforced, meaning divergence between the two is a blocking merge error
rather than a discipline problem. It is offered as a synthesis of established software
engineering principles rather than a new paradigm, with machine enforcement as its distinguishing
characteristic: properties that classical approaches left to discipline are encoded as blocking gates
and deterministic derivations.

## Usage

The framework is organized around five interlocking components — a spec graph, a context assembler,
a drift validator, governance gates, and a capability registry — operated by four actors with distinct
authority. The vertical-slice growth protocol described below governs how the graph grows; the paper's
concluding summary counts it among the engine's mechanisms in place of the registry.

**The spec graph** makes every architectural entity a node, materialised as exactly one specification
file whose kind field declares its level, with nodes organized at four zoom levels from system down to
code. Each node carries two orthogonal views: an outward contract, which neighbours may read, holding
public interfaces, invariants, types, error behaviour and acceptance criteria; and an inward design,
visible only to the node's implementer and its parent, holding the internal approach and code
ownership. Two edge types are distinguished: ownership edges form a tree in which a parent's contract
is the sum of its children's, and dependency edges form a directed acyclic graph in which a node may
use another's contract but never its design or code.

**The Spine** is the ownership path from the graph root to the node currently being worked on, and it
is what bounds agent context. The bundle assembled for an agent is the root invariants, the contracts
along that path, the node's own full specification and code, and the contracts of its declared
dependencies one hop only. It excludes sibling components, dependency designs, dependency code,
transitive dependencies and ad-hoc search results. The assembler is a deterministic function over the
graph rather than a search: where the bundle is insufficient, it reports a structured diagnostic —
missing contract, undeclared dependency, missing acceptance criterion — rather than falling back to
free search, and the prescribed repair is to fix the graph rather than widen the context. Cross-cutting
invariants that would otherwise have to be replicated at every node instead live in a single
architecture document that sits transversally to the tree and is prepended to every bundle.

**The vertical-slice growth protocol** governs how the system grows, under a two-layer rule. Layer 1
fixes root invariants and key container boundaries deliberately and up front; Layer 2 grows features
as hardest-first vertical slices, each a thin end-to-end increment. Six growth rules classify each
change — behaviour, decomposition, dependency, boundary, internal design, and promotion to a higher
zoom level — and prescribe the minimal coupled set of artefacts to update. Two properties follow:
decomposition is contract-preserving, because children's contracts sum to the parent's, and
internal-only changes do not ripple into neighbour specifications.

**The drift validator** derives two graphs and compares them — an intent graph from the specification
files and an evidence graph from static analysis of the code, covering imports and exports, routes and
events, and tests. Some divergences block a merge unconditionally; weaker signals, such as a declared
dependency with no code evidence or contract behaviour without test evidence, are reported as
warnings.

**Governance gates** tie review to a change's blast radius and reversibility across three gate
levels: human approval before merge, agent proceeds with asynchronous human review, and engine policy
alone. Four actors operate the engine with separated authority — a human architect with decision
rights over boundaries and public contracts, a planner agent proposing decomposition, a coding agent
implementing within its bundle, and the engine itself, which is deterministic and authors no intent.

**The capability registry** is the framework's horizontal reuse axis. A capability carries a stable
identifier and has exactly one providing node, and an agent about to implement one queries the registry
first, so that two nodes providing the same capability are flagged as duplicates — a check the author
describes as DRY at the architecture level.

## When It Applies

The framework addresses two failure modes its author identifies in AI-assisted development —
unscoped agent context and specification drift that accumulates unnoticed — and its applicability
follows from those rather than from any stated threshold of project size or age. Its author positions
it between spec-first
approaches, which discard or defer the specification after generation, and spec-as-source approaches,
which generate code from the specification and which the author argues buy synchronization at the cost
of nondeterminism.

It assumes a static dependency graph can be derived from source files — imports, routes, events — which
its author names as a limitation: highly dynamic systems such as those using runtime dependency
injection or plugin architectures require late-bound dependencies to be annotated explicitly. The
governance overhead is acknowledged as real for fast-moving teams, mitigated but not eliminated by the
middle gate level. The stated artefact cost is one specification file per architectural node at
component level or above, plus one architecture document per system, which the author argues is
substantially less than traditional architecture documentation and is partially offset by the context
savings of a scoped bundle.

How well established it is, the source settles only on one side: the mechanisms it composes are drawn
from long-standing software engineering work, but the engine itself is a design proposal by a single
author with no experiment, benchmark or user study reported, and its worked example illustrates the
machinery rather than measuring it. The author states it is maintained as an internal design-document
set with a public release planned.

## Related Terms

- [[ScholarlyArticle/the-spec-growth-engine]] — the paper that proposes this framework
- [[DefinedTerm/spec-driven-development]] — the broader practice this framework is a variant of
- [[DefinedTerm/context-blindness]] — a closely related failure mode named by a different source, in
  which an agent's artifacts are coherent but incompatible with the repository
- [[DefinedTerm/context-rot]] — the degradation with input length that motivates the Spine's scoping
