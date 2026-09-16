---
title: "Agentic Autonomy Levels"
type: "schema:BlogPosting"
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
  description: "A proposal for measuring AI coding agent autonomy along two separate axes, agency and orchestration, replacing a single-axis ladder, and a six-level scale built from combining them."
  author: "Addy Osmani"
  datePublished: "2026-07-02"
---

This post argues that discussions of AI coding agent autonomy have historically conflated two separate questions — how far a single agent is allowed to go on its own (agency), and how well multiple agents are coordinated (orchestration) — and that a single-axis autonomy ladder, such as the one popularized by Steve Yegge, cannot represent both. It proposes measuring the two axes separately and then presents the [[DefinedTerm/agentic-autonomy-levels]] scale: six levels that read as a single climb because orchestration only becomes a factor near the top of the scale.

The post also argues that risk and reversibility, not task type, should set the ceiling on how much autonomy is applied to a given task, and proposes a "contract" of named fields (goal, scope, non-goals, tools/permissions, stopping condition, evidence, escalation, budget) that should precede any agent run.

## Key Points

- The autonomy ladder is split into two axes — agency (how far one agent goes) and orchestration (how many agents run and who coordinates them) — because a single number cannot represent both, and orchestration is described as mattering only near the high end of the scale.
- Six levels are defined, from Level 0 (Assist, where a human decides whether to act on every suggestion) through Level 5 (Managed-by-exception orchestration, where a manager agent dispatches and monitors worker agents against defined policies and escalates only exceptions to a human).
- The post cites two Anthropic research write-ups: one finding Claude Code asked for clarification more than twice as often as users interrupted it, and a second, covering roughly 400,000 sessions from about 235,000 people between October 2025 and April 2026, finding that people make about 70% of planning decisions while Claude executes about 80% of actions.
- Three diagnostic questions are proposed for judging whether an agent is actually operating with high autonomy: how quickly a wrong action would be noticed, how cleanly it could be undone, and what would prove the action was right.
- Four autonomy anti-patterns are named: "autonomy as status" (treating a high autonomy rating as a badge rather than a safety judgment), "permission laundering" (granting broader access than needed due to approval fatigue), "summary substitution" (letting an agent's own summary stand in for review), and "fleet cosplay" (running many agents in parallel while a human still coordinates every dependency by hand).
- The post states the article itself is labeled by Pangram as 100% human-written, per a linked verification record.

## Context

The post explicitly builds on and revises Steve Yegge's single-axis autonomy ladder (described in "Welcome to Gas Town" and covered by The Pragmatic Engineer), presenting the two-axis agency/orchestration model as a correction for a gap the single-axis version cannot capture once multi-agent orchestration becomes common. It also references OpenAI's proposed Symphony orchestration design as one example of the operating-system-like layer its Level 5 describes.
