---
title: "Inside the Scaffold: A Source-Code Taxonomy of Coding Agent Architectures"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, agent-architecture, surveys, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.03515'
    hash: sha256:5afdaed7652dc3b8c3833fd90b9e8d54cd5d758f847d5d80b3aee353a3cb3acd
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A source-code-level architectural taxonomy of 13 open-source coding agent scaffolds, analysed at pinned commit hashes across 12 dimensions in three layers. Its central finding is that scaffold architectures occupy continuous spectra and compose loop primitives rather than falling into discrete categories."
  author: ["Benjamin Rombaut"]
  datePublished: "2026-04-10"
  abstract: "LLM-based coding agents can localize bugs, generate patches, and run tests with diminishing human oversight, yet the scaffolding code that surrounds the language model — the control loop, tool definitions, state management, and context strategy — remains poorly understood. Existing surveys classify agents by abstract capabilities that cannot distinguish between architecturally distinct systems, and trajectory studies observe what agents do without examining the scaffold code that determines why. The paper presents a source-code-level architectural taxonomy derived from analysis of 13 open-source coding agent scaffolds at pinned commit hashes, characterizing each across 12 dimensions organized into three layers: control architecture, tool and environment interface, and resource management."
---

This paper asks a question that the existing literature on coding agents mostly skips: not what
agents do at runtime, but what the code around the model actually looks like. The author's argument
for the gap is concrete — under capability-based taxonomies (tool-using, memory-augmented, planning,
reflective) every agent in the corpus qualifies for every category, so an agent that runs Monte Carlo
Tree Search over candidate patches and one that runs a while loop with test-driven retries come out
indistinguishable, despite differing in ways that affect cost, reliability and failure modes.

The method is a qualitative case study. Thirteen open-source coding agents were selected from an
initial pool of 22 candidates under three inclusion criteria — coding-specific rather than
general-purpose, open source with a readable and commit-pinnable implementation, and architecturally
distinct from the others — and each was analysed at a pinned commit hash. The analysis framework
began with six dimensions drawn from the conceptual agent-architecture literature and grew to nine
through iterative open coding during a pilot on two deliberately contrasting agents, Aider and
[[SoftwareApplication/openhands]]; those nine map to 12 taxonomy dimensions in the results: two
sub-properties — loop driver, and edit and patch format — proved discriminating enough to be
presented separately, and a third dimension, control flow implementation, emerged during analysis as
an axis of variation orthogonal to loop topology and is likewise presented independently. Every taxonomic
claim is grounded in file paths and line numbers. The paper deliberately does not benchmark agent
performance, on the argument that benchmark scores confound scaffold architecture with model
capability, prompt engineering and incidental configuration.

The 12 dimensions are organised into three layers: **control architecture** (how the agent decides
what to do next), **tool and environment interface** (how it interacts with code and execution
environments), and **resource management** (how it manages context, state and models).

## Key Points

- The paper's headline finding is that scaffold architectures resist discrete classification and are
  better described as positions along continuous spectra: control strategies range from a fixed
  pipeline with no feedback loop to full Monte Carlo Tree Search with reward backpropagation, tool
  counts from 0 to 37 action classes, and context compaction across seven distinct strategies.
- It identifies five **loop primitives** — ReAct, generate-test-repair, plan-execute, multi-attempt
  retry, and tree search — that function as composable building blocks rather than mutually exclusive
  types, and reports that 11 of the 13 agents layer multiple primitives rather than relying on a
  single control structure.
- Because the primitives compose freely, it argues the space of possible architectures is
  combinatorial rather than categorical, and draws the methodological consequence that evaluating
  scaffold dimensions independently is more informative than classifying whole agents.
- It treats **loop driver** — who decides what happens next — as arguably the most fundamental
  architectural distinction, and separates user-driven, scaffold-driven and LLM-driven designs. It
  observes that user-driven agents sidestep the bug-localisation bottleneck identified in prior
  trajectory analyses, because if the user selects files then incorrect localisation is a user error
  rather than an agent failure.
- Semantic loop type and code-level implementation are orthogonal: the same taxonomy separates the
  loop's topology from the four mechanisms that realise it — imperative while loops (8 of 13 agents),
  recursion, graph-as-control-flow via a compiled state machine, and exception-based signalling.
- Raw tool counts obscure a convergence in what tools actually do: the same four capability
  categories — read, search, edit, execute — appear across all LLM-driven agents in the corpus, with
  low-tool agents achieving coverage through composition and high-tool agents decomposing the same
  categories into finer-grained operations.
- Context compaction divides into two philosophies the paper labels **prevention** and **cure**:
  prevention agents bound context growth structurally through per-node message scoping, round limits
  or tree depth, while cure agents let context grow and compress it when a token threshold is
  reached. Prevention avoids summarisation cost and information loss but requires the scaffold to
  anticipate growth patterns.
- It distinguishes **sampling** from **iteration** as two fundamentally different responses to a
  failed patch — generate another independent attempt, or refine the failed one using feedback — and
  notes this cuts across the control-loop taxonomy because it describes how agents handle the
  population of solution attempts rather than the structure of any single attempt.
- It separates two selection problems that tree-search agents face and that can be solved by the same
  mechanism or different ones: **online guidance** (which branch to explore next during the search)
  and **offline selection** (which completed solution to return afterwards).
- Converging and diverging dimensions carry different information. Dimensions converge where external
  constraints dominate — tool capability categories, edit format, execution isolation — and the paper
  reads these as solved problems and candidates for standardisation. Dimensions diverge where open
  design questions remain — context compaction, state management, multi-model routing — and it argues
  this divergence is not noise but genuine uncertainty about the best approach, marking where
  research investment is most needed.
- Cost optimisation is reported as the primary driver of multi-model routing among the agents that
  use several models, with mechanical tasks routed to cheaper models and expensive ones reserved for
  reasoning.
- The paper reads the coexistence of fork-based and dependency-based reuse of the same upstream
  project as evidence that the ecosystem has not yet stabilised around clean extension points.

## Notes

The paper positions itself against three neighbouring literatures. Conceptual agent-architecture
surveys supply useful vocabulary but operate at an abstraction that cannot separate production
systems. Trajectory and behaviour studies establish empirical regularities but treat agents as black
boxes, observing what agents do without explaining why — and, the author notes, prior trajectory work
compared agents running on different underlying models, which confounds scaffold effects with model
effects. Detailed architectural descriptions exist for individual systems but leave the design space
as a whole unmapped.

The author also distinguishes this work from research on how developers *configure* coding agents,
describing the two as complementary: configuration artifacts control what instructions the agent
receives, while scaffold architecture determines how the agent processes those instructions.

The taxonomy is offered as enabling future controlled experiments by naming the variables that would
need to be held constant — for instance comparing agents with identical tool sets but different loop
strategies, with the model held fixed.

See [[DefinedTerm/agent-scaffold]] for the subject itself, and [[DefinedTerm/compaction]] for one of
the dimensions the paper places among its diverging ones.
