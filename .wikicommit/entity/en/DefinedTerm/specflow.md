---
title: "Specflow"
type: "schema:DefinedTerm"
lang: en
tags: [spec-driven-development, agentic-coding, software-development-process]
sources:
  - type: url
    url: 'https://specstory.com/whitepapers/beyond-code-centric-specstory-2025.pdf'
    hash: sha256:4dc1c2f09b2ea2dff0c8bfb3cc6e5eb177c4c5134a96a0025cf03ad6841972e8
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "SpecStory's named five-step workflow for converting intent into software with coding agents — pre-plan, roadmap, workplans, execute, update and refine — run on top of trunk-based development and adding declared intent as a layer alongside code and tests."
---

Specflow is a workflow published by [[Organization/specstory]] for converting intent into software through structured planning and iterative execution with coding agents. Its own description of itself is "an open, flexible workflow", formalised, according to [[Report/beyond-code-centric]], after thousands of hours using agents with Cursor, Copilot and Claude Code. It is designed to run on top of trunk-based development rather than to replace a branching model, and its governing principle is stated as "plan first, act second".

## Usage

The workflow has five steps. At **pre-plan**, product managers define user outcomes, designers add patterns and engineers list constraints, with a top reasoning model helping synthesise the result. At **roadmap**, everyone co-authors a markdown roadmap kept in the repository. At **workplans**, each roadmap phase is broken into human- and AI-executable tasks, which the whitepaper describes as the step that forces implicit knowledge out into the open. At **execute**, agents tackle the tasks, and anyone can intervene because the context lives in git. At **update and refine**, the documents evolve with each cycle, capturing decisions and as-built truth in shared project memory.

What distinguishes it from the emergent-design tradition, on its publisher's account, is a third layer. Code and tests still serve as specifications, but agent-first development adds declared intent — roadmaps, workplans and docs, all in markdown — that both humans and AI can interpret.

The failure mode it is positioned against is what the whitepaper calls ad-hoc adversity: without this structure, vague prompts yield incorrect outputs, repeated revisions, regressions, difficult integrations and unmanageable technical debt, with [[DefinedTerm/vibe-coding]] "by multiple roles in multiple places" producing fragmented results that do not align. The diagnosis offered is context loss — each AI prompt is relatively stateless, so without shared structure the system does not converge, and scattered instructions from multiple team members compound the fragmentation.

Its publisher is explicit that the workflow redistributes complexity rather than removing it, and lists the residual costs as decisions a seasoned developer would otherwise handle by intuition: deciding what context to load before any prompt, choosing which model suits each stage, making explicit the scope assumptions humans normally leave unspoken, and judging when to interrupt an agent mid-task. On the last of these it notes that an early stop wastes potential progress while a late stop produces a large tangle to unravel, and that progress tracking becomes explicit too, since done criteria, commit points, branching and documentation policies must all be defined rather than sensed.

All of this is the workflow publisher's own account of its own method. The outcome it reports — three people delivering a complete end-to-end macOS alpha of SpecStory's Studio product in four weeks — is a first-party figure with no independent verification.

## Related Terms

Specflow is one concrete implementation of [[DefinedTerm/spec-driven-development]], and sits alongside other named workflows for the same general idea rather than defining it.
