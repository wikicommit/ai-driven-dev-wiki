---
title: "Agentic Autonomy Levels"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agentic-autonomy-levels/'
    hash: sha256:6461372eb41776e02b97a60cc7bd705cbee5b8f388dbb6b61b2a3ed54963d8f7
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A six-level classification scheme for AI coding agent autonomy, built from two separate axes — agency (how far a single agent goes) and orchestration (how many agents run and who coordinates them) — rather than a single ladder."
---

Agentic Autonomy Levels is a six-level scheme for classifying how autonomously an AI coding agent (or fleet of agents) operates, built from two axes measured separately: agency, how far a single agent is allowed to go before a human decision is required, and orchestration, how many agents run and who coordinates them. The two axes are read together as one climb because, in this scheme, orchestration only becomes a distinguishing factor near the top of the scale.

## Usage

The six levels are: **Level 0 (Assist)** — the agent suggests actions and a human decides on every one; **Level 1 (Supervised action)** — the agent edits or runs commands but asks before anything consequential; **Level 2 (Scoped task delegation)** — a bounded task with a clear goal and definition of done is handed off, verified by evidence such as passing tests; **Level 3 (Goal-driven autonomy)** — the agent does whatever it takes to reach a goal defined by a measurable, automatable stopping condition; **Level 4 (Parallel delegation)** — multiple agents work isolated slices of a task in parallel; and **Level 5 (Managed-by-exception orchestration)** — a manager agent dispatches worker agents against defined policies, verifies their output, and escalates only exceptions to a human.

The scheme is presented as a two-axis alternative to Steve Yegge's earlier single-axis autonomy ladder (from "Welcome to Gas Town"), on the grounds that a single number cannot separately represent an individual agent's trust level and an organization's skill at coordinating many agents at once.

## Related Terms

[[BlogPosting/agentic-autonomy-levels]]
