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
  - type: url
    url: 'https://addyosmani.com/blog/good-spec/'
    hash: sha256:fbb1e0c078b1d920689cbc3c652ad4bf253d5b39c77f957cab7ee4e6cd1ff5fa
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Driving a coding agent from a written task specification rather than directly from a prompt: the prompt is first turned into a specification, which is refined and optionally reviewed by a human, and only then implemented."
---

Spec-driven development is the practice of putting a written specification between a developer's
prompt and an agent's implementation, so that what the agent builds from is a reviewed artefact
rather than the original request. The prompt is first turned into a specification; that
specification is analysed and refined, and can be corrected by a human before anything is built;
implementation then proceeds from the specification and is verified against it. Two independent
accounts of the practice are described here — a plugin implementation and a tool-vendor-published
workflow — and they agree on this much while differing in the concrete mechanics below.

## Usage

**The Spec-Driven Development plugin in [[SoftwareApplication/context-engineering-kit]]** reduces the
practice to three commands: one creates a task file from an initial prompt, one analyses the prompt
and iteratively refines the specification until it meets a quality bar, and one produces a working
implementation from the resulting file and verifies it. The project characterises the result as
development as compilation — task specification in, working code out — and suggests clearing the
agent's session between planning and implementation so the second step starts on a fresh context.
Planning is split across specialised sub-agents for research, codebase exploration, requirements and
acceptance criteria, architecture, and decomposition into independently verifiable steps;
implementation runs per step, with review at the end of each phase. Its specification format is
based on arc42, which the project calls a widely adopted standard for software development
documentation, adjusted for what an LLM can act on by removing parts the project judges to add
nothing to implementation quality. Around the core loop sit optional refinements: a `--refine` flag
to re-run planning after a human has edited or commented on the specification, a
`--human-in-the-loop` flag to gate each planning and implementation phase, and the ability to declare
dependencies between tasks so that a large piece of work can be decomposed into separately specified
units.

**GitHub's Spec Kit**, described in a separate source, structures the same core idea as four gated
phases — Specify, Plan, Tasks, Implement — where a human does not move to the next phase until the
current one is validated. Specify covers user journeys and success criteria rather than technical
stack; Plan is where the developer supplies architecture, stack, and constraints for the agent to turn
into a technical plan; Tasks breaks the spec and plan into small, independently reviewable and
testable chunks; and Implement works through those tasks one by one (or in parallel), with the
developer reviewing focused changes rather than large code dumps at the end. That source frames the
specification, once approved, as a persistent, version-controlled artefact fed back into the agent's
context across sessions, comparable to a team's Product Requirements Document.

## When It Applies
The practice trades developer time and tokens for reliability, so it applies where that trade is
worth making. The context-engineering-kit project positions it for complex or large codebases with
existing structure — arguing that, unlike frameworks aimed at greenfield work, it performs better the
more existing code there is, because each planning phase includes an analysis of which files a
change would affect and which patterns to follow. Its own comparison places the specification-driven
route at the reliable end of a progression that starts with a one-shot prompt, and puts the token
overhead at a multiple of the baseline, rising further with human review.

It assumes that a specification is worth writing at all, and that the developer will invest in it.
The context-engineering-kit project is explicit that quality is highly proportional to the time spent
iterating on the specification, and that without human feedback the result will be working but
sub-optimal — by default the plugin makes its own assumptions rather than asking for clarification,
on the reasoning that developer time is more valuable than model time. The failure mode it reports is
not a broken build but wasted effort: when the initial specification was wrong because of missing
information or task complexity, the agent still self-corrected to a working solution, but took much
longer and spent time on wrong paths, which is why it advises decomposing work into smaller tasks and
reviewing each specification independently.

The GitHub Spec Kit account frames the same trade differently: its four gated phases exist to prevent
what that source, citing Simon Willison, calls "house of cards code" — fragile AI output that
collapses under scrutiny — by refusing to let implementation start until the spec and plan are
validated. In that account's Plan phase specifically, a company's standardized technology choices,
legacy-integration constraints, or compliance requirements are what the developer supplies for the
agent to fold into the technical plan.

How well established the practice is, neither source settles. Each uses the term for its own
implementation and for the pattern that implementation embodies; the context-engineering-kit's
reliability claims — including that its plugin produced working code in every case its team tested —
are the project's own, based on internal production use rather than independent evaluation. The
GitHub Spec Kit account comes from a third-party blog post citing GitHub's own published study and
documentation of the tool, rather than from an independent evaluation of it.

## Related Terms
- [[DefinedTerm/vibe-coding]] — the practice the project contrasts its plugin with: it describes
  the plugin as not a vibe-coding solution while noting that out of the box, driven from a single
  prompt with no human checkpoints, it behaves like one
- [[DefinedTerm/subagent-driven-development]] — the lighter-weight approach the same project offers
  as a distilled version of this one
- [[DefinedTerm/llm-as-a-judge]] — the evaluation technique used for the quality gates between
  phases
- [[BlogPosting/good-spec]] — source of the GitHub Spec Kit account of this practice
- [[DefinedTerm/three-tier-boundaries]] — a related spec-writing pattern from the same source
