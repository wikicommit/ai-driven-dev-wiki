---
title: "Agent Scaffold"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, coding-agents, agent-tooling]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.03515'
    hash: sha256:5afdaed7652dc3b8c3833fd90b9e8d54cd5d758f847d5d80b3aee353a3cb3acd
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The code surrounding a language model in a coding agent — the control loop, tool definitions, state management and context strategy — that determines how the agent behaves, what mistakes it makes and where it spends its token budget."
---

An **agent scaffold** is the scaffolding code that surrounds the language model in a coding agent:
the control loop, the tool definitions, the state management and the context strategy.
[[ScholarlyArticle/inside-the-scaffold]] argues that as agents move from research prototypes to
production tooling, this code increasingly determines how the agent behaves, what mistakes it makes,
and where it spends its token budget — and that it nevertheless remains poorly understood in the
research literature, because conceptual surveys classify agents by abstract capabilities rather than
by the implementation strategies that distinguish one production system from another.

## Usage

That paper's taxonomy, derived from source-code analysis of 13 open-source agents, organises scaffold
design into three layers.

**Control architecture** — how the agent decides what to do next. It covers the topology of the
control loop, which the paper places on a spectrum from a fixed pipeline with no feedback loop
through user-driven loops, sequential ReAct loops and phased loops to depth-first tree search and
full Monte Carlo Tree Search; the loop *driver*, meaning whether the user, the scaffold or the model
decides what happens next; and the code-level mechanism that implements the loop, which may be an
imperative while loop, recursion, a compiled state machine, or exception-based signalling.

**Tool and environment interface** — how the agent interacts with code and execution environments. It
covers the tool set and how tools are communicated to the model, the edit and patch format, whether
tools are registered statically at startup or discovered dynamically, the context-retrieval paradigm
(model-directed tool calls, precomputed indexes, embedding search, or a static repository map), and
the execution isolation model, which records the trust boundary between the agent and the host.

**Resource management** — how the agent manages context, state and models. It covers the state
management strategy (the data structure holding history, and whether it is append-only or mutable),
the context compaction approach, multi-model routing, and persistent memory across sessions.

The same paper argues that these dimensions are best treated as continuous spectra, and that five
**loop primitives** — ReAct, generate-test-repair, plan-execute, multi-attempt retry and tree
search — act as composable building blocks that agents layer and nest, so that the space of possible
scaffolds is combinatorial rather than categorical.

## When It Applies

- Applies to any design decision made outside the model: which tools to expose and at what
  granularity, how history is represented, when to compress it, where code runs, and which model
  handles which step. The paper's framing is that the same underlying model behaves differently
  depending on these choices, so they mediate model capability rather than merely supporting it.
- Assumes the scaffold and the model can be reasoned about separately. The paper is explicit that
  this assumption is often violated in practice — it declines to benchmark the agents in its corpus
  on the grounds that benchmark scores confound scaffold architecture with model capability, prompt
  engineering and incidental configuration such as iteration limits and cost caps.
- Fails as an analytical frame when it is collapsed into a single label. The paper's argument is that
  assigning one name ("ReAct agent", "pipeline agent") to a system layering several primitives
  obscures the decisions that actually differentiate it, and that a study comparing such labels
  conflates loop topology, loop driver, tool set design and context management into a single binary.
- Not uniformly settled. The paper distinguishes dimensions that have converged, where external
  constraints dominate and practitioners have arrived at common answers, from dimensions that remain
  divergent because no dominant solution has emerged — naming context compaction, state management
  and multi-model routing in the second group.
- Grounded in a single-researcher qualitative case study of 13 agents selected non-exhaustively from
  an initial pool of 22, with every claim pinned to file paths and line numbers at fixed commits.
  Its findings describe the open-source corpus it examined as of early 2026; proprietary agents whose
  scaffold code is not inspectable were excluded by construction.

## Related Terms

- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/agent-computer-interface]]
- [[DefinedTerm/compaction]]
- [[DefinedTerm/agent-execution-environment]]
- [[DefinedTerm/react-prompting]]
- [[DefinedTerm/sub-agent-architecture]]
- [[DefinedTerm/ai-coding-agent]]
