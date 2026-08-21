---
title: "Spine"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, architecture, spec-driven-development, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.27045'
    hash: sha256:9004fd8330acfa64f27d8cc588f1234dd91b29303e4ee479b537bbdebca481f6
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The ownership path from a spec graph's root to the node an agent is working on, used as a deterministic scope for that agent's context bundle instead of free repository search."
  termCode: ""
  inDefinedTermSet: ""
---

The Spine, as defined in [[ScholarlyArticle/the-spec-growth-engine]], is the ownership path from the root of a specification graph down to the node an agent is currently working on: root → … → parent(N) → N. It is used as the scope for that agent's context, replacing free-form repository search with a deterministic traversal.

Its stated design principle is Parnas information hiding applied to agent context: the same boundary that hides a module's design from its neighbours also limits what the coding agent for that module is allowed to attend to.

## Usage

The Spine is meant to answer three questions an agent needs but must not answer by searching the repository itself: *why does this node exist* (the higher-level promise it supports), *what constraints must it obey* (root invariants propagated downward), and *what may it use* (the contracts — not designs — of its declared dependencies, one hop only).

The context bundle it produces is composed of root invariants, the contracts along the ownership path, the working node's full specification, the contracts of its declared dependencies, and the node's own code. What the paper emphasises is the exclusion list: sibling components, dependency designs, dependency code, transitive dependencies, and ad-hoc grep results are all left out. Its stated rule is that the assembler determines what the agent reads and the agent does not search freely.

The assembler is a deterministic function of the node and the graph. Where the bundle turns out to be insufficient for a task, it reports a structured diagnostic — a missing contract, an undeclared dependency, a missing acceptance criterion — rather than silently falling back to free search; the paper's stated default repair is to fix the spec graph, not to widen the context.

Cross-cutting invariants sit outside the ownership tree, because replicating them at every node would be unworkable. A single `ARCHITECTURE.md` sits transversally and is prepended to every context bundle automatically: it is not a node, has no owner, and belongs to every node simultaneously. That mechanism is what makes an architecture-wide invariant visible to every node by construction, and therefore enforceable by the drift gate.

## Related Terms

The Spine is that framework's answer to context degradation under long inputs — see [[DefinedTerm/context-rot]] — and a concrete instance of [[DefinedTerm/context-engineering]] in which scoping is derived from architecture rather than from retrieval heuristics. It is the counterpart to that same framework's [[DefinedTerm/spec-code-drift]] gate: one bounds what the agent reads, the other bounds what it may leave behind.
