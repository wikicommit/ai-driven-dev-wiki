---
title: "Building Effective AI Coding Agents for the Terminal: Scaffolding, Harness, Context Engineering, and Lessons Learned"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, context-engineering, agent-architecture, agent-safety]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05344'
    hash: sha256:29a5dfd46c7505affc599f6922ebba2f67d01e7f3a343df5347a42f435a08edc
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A technical report on OPENDEV, an open-source terminal-native coding agent, documenting its four-layer architecture and the design trade-offs behind it, and generalising five cross-cutting tensions — context pressure, behavioural steering over long horizons, safety through architectural constraint, designing for approximate model output, and bounding resources that grow with session length."
  author: ["Nghi D. Q. Bui"]
  datePublished: "2026-03-13"
  keywords: ["Artificial Intelligence", "Coding Agents", "Context Engineering"]
  citation: "arXiv:2603.05344"
---

This report documents the engineering of [[SoftwareApplication/opendev]], an open-source
command-line coding agent, and is presented by its author as the first comprehensive technical
report for an open-source, terminal-native, interactive coding agent. Its stated premise is that AI
coding assistance has shifted away from IDE plugins toward terminal-native agents that sit where
developers already run source control, builds and deployments — a shift the paper credits Claude
Code with leading — and that the design space for such agents remains underexplored because
production systems are closed-source with undocumented decisions, while open frameworks either
target benchmarks rather than interactive use or publish no technical report. The paper is explicit
that its purpose is to share design decisions, trade-offs and lessons rather than to present an
algorithmic result.

The architecture is organised into four layers — entry and UI, agent, tool and context, and
persistence — and around a distinction the paper draws between *scaffolding*, which assembles the
agent before the first prompt, and the *harness*, which orchestrates tool dispatch, context
management, safety enforcement and persistence at runtime. A central framing is that the system is a
compound AI system rather than a single model: work is organised as a four-level hierarchy of
session, agent, workflow and LLM, so that each cognitive workflow binds independently to a
user-configured model and cost, latency and capability can be traded off per workflow. The paper
presents five contributions on this basis: per-workflow LLM configurability, an extended ReAct loop
with explicit thinking and optional self-critique phases, event-driven system reminders,
token-efficient extensibility with a five-layer safety architecture, and context engineering treated
as a first-class concern.

The second half generalises from the system to five cross-cutting design tensions, each stated with
a transferable lesson. The report gives concrete figures for several of them: tool outputs consume
70–80% of context in a typical session; instructions that govern the agent's first turns are
routinely violated after thirty or more tool calls; loading all MCP tool schemas eagerly consumed
40% of the context budget before the first user message, which lazy discovery reduced to under 5%;
and adaptive context compaction, which moves observations through active, faded and archived states,
reduced peak context consumption by roughly 54%.

## Key Points

- The report distinguishes scaffolding — assembling the system prompt, tool schemas and subagent
  registry before the first prompt — from the harness, which orchestrates tool dispatch, context
  management, safety enforcement and session persistence at runtime, and argues the two should be
  kept separate so each can evolve independently.
- It frames the agent as a compound AI system with a session → agent → workflow → LLM hierarchy, so
  that switching providers or optimising cost is a configuration change rather than a code change.
- It reports that tool outputs — file contents, command results, search hits — consume 70–80% of the
  context in a typical session, and argues context utilisation is the single most important metric
  for how long a session stays useful.
- It argues for graduated context reduction rather than one emergency compaction at a hard limit,
  and reports that adaptive compaction moving observations through active, faded and archived states
  cut peak context consumption by about 54% and often avoided LLM summarisation entirely.
- It recommends offloading oversized tool output to a scratch file and returning a short preview plus
  a file reference, on the grounds that retrieval is paid once while context consumption is paid on
  every subsequent model call.
- It states that local token counting systematically underestimates real usage because providers
  inject invisible content, and that in this system the gap was large enough to trigger compaction
  too late and cause overflow; the provider's reported token count should be treated as ground truth.
- It argues safety is better enforced by removing tools from the agent's schema than by checking
  permissions at call time, since a model cannot argue for or probe around a capability it never
  sees, and describes five independent safety layers so that no single bypass compromises the system.
- It reports that short reminders injected at the point of decision outperform long system prompt
  sections, that reminders sent in the user role produced stronger compliance than the system role in
  the author's experiments, and that reminder frequency must be capped per type or the model learns
  to ignore them.
- It reports that giving the model a thinking phase with no tools available produces substantially
  better reasoning than instructing it to think carefully while tools are present, and attributes the
  effect to the absence of tool schemas from the API call rather than to the instruction.
- It argues that tools should absorb the model's imprecision — a chain of progressively relaxed
  matchers for edits, recovery hints checked against the tools the agent actually has — rather than
  demanding exact correctness and spending the session in error-recovery loops.
- It states that the system's specific thresholds — a 70% compaction trigger, three nudge attempts,
  six thinking depth levels — emerged from iterative failure analysis rather than from
  first-principles calculation, and recommends that approach.
- It presents no quantitative benchmark evaluation, naming evaluation on SWE-bench, Terminal-Bench
  and LongCLI-Bench as future work alongside adaptive resource allocation, a scaled memory pipeline,
  structured code representations for memory, and multi-agent coordination beyond hierarchical
  delegation.

## Notes

This is a design-and-lessons report on one system by its own author, and it says so: it documents
architectural decisions and rationale and explicitly lacks systematic quantitative evaluation, so
the figures it gives — the 54% reduction in peak context consumption, the fall in MCP schema
overhead from 40% to under 5%, the 70–80% share taken by tool outputs — are measurements of this
system in the author's own use rather than results established against a baseline. The claims about
reminder role and about separating thinking from action are likewise reported from the author's
experiments without an accompanying experimental protocol.

The report positions itself against neighbouring systems by what they publish rather than by
measured comparison: benchmark-oriented frameworks that have papers but target automated
evaluation, a production-grade documented system that runs through a browser UI rather than a
terminal, several CLI-native agents with no published technical report, and Claude Code as
CLI-native but neither open-source nor accompanied by one.
