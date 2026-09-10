---
title: "Spec-driven development"
type: "schema:DefinedTerm"
lang: en
aliases: ["SDD", "Specification-driven development"]
tags: [agents, coding-tools, llm, long-horizon-tasks]
sources:
  - type: url
    url: https://github.com/NeoLabHQ/context-engineering-kit
    hash: sha256:3a00d5fa6029f48343ba32101feda4acd0f31870b7ff74ef954be99d4e04a584
    license: GPL-3.0
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "Driving a coding agent from a written task specification rather than directly from a prompt: the prompt is first turned into a specification, which is refined and optionally reviewed by a human, and only then implemented."
---

Spec-driven development is the practice of putting a written specification between a developer's
prompt and an agent's implementation, so that what the agent builds from is a reviewed artefact
rather than the original request. The prompt is first turned into a task specification; that
specification is analysed and refined, and can be corrected by a human before anything is built;
implementation then proceeds from the specification and is verified against it. The account given
here comes from a single implementation — the Spec-Driven Development plugin in
[[SoftwareApplication/context-engineering-kit]] — and describes how that implementation works, not a
settled definition shared across the field.

## Usage
In that implementation the practice is reduced to three commands: one creates a task file from an
initial prompt, one analyses the prompt and iteratively refines the specification until it meets a
quality bar, and one produces a working implementation from the resulting file and verifies it. The
project characterises the result as development as compilation — task specification in, working code
out — and suggests clearing the agent's session between planning and implementation so the second
step starts on a fresh context. Planning is split across specialised sub-agents for research,
codebase exploration, requirements and acceptance criteria, architecture, and decomposition into
independently verifiable steps; implementation runs per step, with review at the end of each phase.

The specification format is not invented for the purpose. The project's template is based on arc42,
which the project calls a widely adopted standard for software development documentation, adjusted for what an LLM can act on
by removing parts the project judges to add nothing to implementation quality. Around the core loop
sit optional refinements: a `--refine` flag to re-run planning after a human has edited or commented
on the specification, a `--human-in-the-loop` flag to gate each planning and implementation phase,
and the ability to declare dependencies between tasks so that a large piece of work can be
decomposed into separately specified units.

## When It Applies
The practice trades developer time and tokens for reliability, so it applies where that trade is
worth making. The project positions it for complex or large codebases with existing structure —
arguing that, unlike frameworks aimed at greenfield work, it performs better the more existing code
there is, because each planning phase includes an analysis of which files a change would affect and
which patterns to follow. Its own comparison places the specification-driven route at the reliable
end of a progression that starts with a one-shot prompt, and puts the token overhead at a multiple
of the baseline, rising further with human review.

It assumes that a specification is worth writing at all, and that the developer will invest in it.
The project is explicit that quality is highly proportional to the time spent iterating on the
specification, and that without human feedback the result will be working but sub-optimal — by
default the plugin makes its own assumptions rather than asking for clarification, on the reasoning
that developer time is more valuable than model time. The failure mode it reports is not a broken
build but wasted effort: when the initial specification was wrong because of missing information or
task complexity, the agent still self-corrected to a working solution, but took much longer and
spent time on wrong paths, which is why it advises decomposing work into smaller tasks and
reviewing each specification independently.

How well established the practice is, this source cannot settle. It uses the term for its own
plugin and for the pattern that plugin implements, and the reliability claims quoted above —
including that the plugin produced working code in every case its team tested — are the project's
own, based on its internal production use rather than on independent evaluation. Everything above
describes one implementation.

## Related Terms
- [[DefinedTerm/vibe-coding]] — the contrasting practice of building without reviewing what the
  model produces; the project describes its plugin as not a vibe-coding solution while noting that
  out of the box, driven from a single prompt with no human checkpoints, it behaves like one
- [[DefinedTerm/subagent-driven-development]] — the lighter-weight approach the same project offers
  as a distilled version of this one
- [[DefinedTerm/llm-as-a-judge]] — the evaluation technique used for the quality gates between
  phases
