---
title: "Planner–Executor–Reviewer"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-ai, multi-agent-systems, agent-architecture, sdlc]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.15245'
    hash: sha256:93a6c8bfd18429d67e8c2a2a4e4865999e141411cc9f548e35302e716c6d558d
  - type: url
    url: 'https://github.com/datawhalechina/self-harness'
    hash: sha256:1cbe56dd3adc95cae9abae32a6356996fc03b56f4bdeb88b44cae256d918dd66
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A multi-agent role-specialisation pattern in which complex software engineering tasks are decomposed across a planning agent, an executing agent and a reviewing agent, often coordinated by an orchestrator."
---

Planner–Executor–Reviewer is a multi-agent role-specialisation pattern in which a complex software engineering task is decomposed into a sequential or graph-based pipeline of agents, each assigned a specific and bounded responsibility. [[ScholarlyArticle/assistance-to-autonomy-agentic-ai-across-the-sdlc]] identifies it as the predominant architecture across the agentic AI literature it surveys, commonly with an Orchestrator agent managing the flow of sub-processes above the three roles, and reports the structure appearing in publications across every phase of the software development life cycle.

## Usage

The stated rationale for the pattern is cognitive load: narrowing each agent's scope is intended to produce more predictable and accurate outcomes than asking a single generalist agent to plan, synthesise and verify at once. In the surveyed systems this is frequently reinforced by structured, typed inter-agent communication — JSON payloads or LangGraph state graphs — replacing free-text handoffs with formally typed state transitions.

The review argues the Reviewer role is not simply a third stage but the pattern's verifiability mechanism: it supplies the feedback that grounds iterative refinement, which is what connects this architecture to [[DefinedTerm/output-verifiability]] as the enabler of agentic adoption more generally.

A two-agent industrial variant illustrates why the separation holds up in practice. In a software release gatekeeping system for automotive software, a Planner applies chain-of-thought reasoning with self-consistency to generate a release strategy, and an Actor executes from a predefined atomic action vocabulary with self-reflection for error correction. The review reports that restricting the Actor to a fixed action set was key to industrial adoption, because it bounds operational risk without sacrificing the Planner's reasoning flexibility — achieving a separation between what to do and how to do it safely.

[[SoftwareApplication/minimaster]], the teaching implementation accompanying the
[[CreativeWorkSeries/self-harness]] tutorial, is a small open-source instance of the same three
roles, arranged as three nested loops: a Planner agent doing global scheduling, an Executor agent
carrying out the work, and a Validator agent assessing it. What it adds sits on the memory side —
the project keeps a separate planner, generator and validation memory, plus a per-task retry archive,
which it presents as the way the necessary context is retained while older trajectories are
compressed. It
pairs the loop with a completion checklist and a guard against the agent repeating an action. This
is tutorial material rather than a deployed system, so it is evidence of how the pattern is taught
and built, not of how it performs.

## When It Applies

The pattern applies where a task is large enough to decompose and where the Reviewer role has something objective to review against. That second condition is the load-bearing one: the review's broader finding is that agentic maturity concentrates in lifecycle phases whose outputs are evaluable through executable feedback, and a Reviewer agent in a phase with no ground-truth signal has only its own judgement to apply.

It assumes each role's responsibility can be bounded cleanly enough that narrowing scope actually reduces error rather than fragmenting context, and — in the industrial variants the review highlights — that the executing agent's action space can be constrained in advance.

The review reports the pattern as dominant across its 92 primary studies, though only 13 of those were evaluated in an industrial context, so the evidence for the constrained-action-space variant in particular rests on a small number of deployments. Beyond role decomposition, the surveyed systems pair the pattern with memory and retrieval architectures, with industrial studies favouring structurally grounded retrieval — hybrid vector-graph representations, or dependency-mapping knowledge graphs used as a shared memory layer across agents — over flat vector retrieval, which loses relational context between artefacts.

## Related Terms

- [[DefinedTerm/output-verifiability]]
- [[DefinedTerm/planner-worker-model]]
- [[DefinedTerm/verification-loop]]
