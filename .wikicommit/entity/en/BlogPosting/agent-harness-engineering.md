---
title: "Agent Harness Engineering"
type: "schema:BlogPosting"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agent-harness-engineering/'
    hash: sha256:7fc8b9bc3a19589c08e3c6ab46607839f3c435799f128886bea9bca6cd634760
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An argument that a coding agent's behavior is dominated by its harness — the scaffolding built around a model — rather than by the model alone, surveying the pieces of that scaffolding and how they combine."
  author: "Addy Osmani"
  datePublished: "2026-04-19"
---

This post argues that "agent = model + harness" (a formulation it attributes to Viv Trivedy), and that most of the leverage in building a capable coding agent sits in the harness rather than in choosing a model. It defines a harness as every piece of code, configuration, and execution logic around a model that gives it state, tool execution, feedback loops, and enforceable constraints, and surveys the harness's component parts: the filesystem and Git, bash and code execution, sandboxes, memory and search, techniques against context rot, long-horizon execution patterns, hooks, and `AGENTS.md`.

The post's central claim is that today's gap between what models can do and what users see them do is largely a harness gap, not a model gap, and it treats every harness component as encoding an assumption about something the underlying model cannot yet do on its own — so a component becomes redundant once a model improves at that specific thing, while a model unlocking a new capability calls for new scaffolding in turn.

## Key Points

- "Agent = Model + Harness. If you're not the model, you're the harness" — a formulation the post attributes to Viv Trivedy, used to argue that the model is one input into a running agent and the rest (prompts, tools, context policies, hooks, sandboxes, subagents, feedback loops, recovery paths) is the harness.
- The post reports that on Terminal Bench 2.0, the same model scored far lower running inside Claude Code's own harness than inside a custom one, and that Viv Trivedy's team moved a coding agent from Top 30 to Top 5 by changing only the harness, not the model.
- Harness engineering is described as treating every agent mistake as a permanent signal rather than a one-off: a failure gets encoded as a rule in `AGENTS.md`, a hook, or a reviewer subagent check, and a rule is only removed once a more capable model has made it redundant.
- Three techniques are named for battling context rot: compaction (summarizing and offloading older context as the window fills), tool-call offloading (keeping only the head and tail of large tool outputs in context and writing the rest to the filesystem), and skills with progressive disclosure (loading instructions and tools only when a task calls for them).
- The post describes the Ralph Loop pattern: a hook intercepts the model's attempt to exit and re-injects the original prompt into a fresh context window, so each iteration starts clean but reads state from the previous one through the filesystem, turning a single-session agent into a multi-session one.
- It cites Anthropic's own published harness-design work for the claim that separating generation from evaluation into distinct agents outperforms self-evaluation, because a model reliably grades its own work more positively than an independent evaluator would.
- It frames "Harness-as-a-Service" (attributed to Viv Trivedy) as a shift from building on LLM completion APIs to building on harness APIs — such as the Claude Agent SDK, the Codex SDK, and the OpenAI Agents SDK — which supply the loop, tools, context management, hooks, and sandbox primitives as a runtime to be customized rather than built from scratch.
- The post argues harnesses do not shrink as models improve; they move — capability gained in one place (e.g. Opus 4.6 reducing anxiety-driven premature wrap-ups) retires some scaffolding while newly reachable tasks require new scaffolding of their own.

## Context

The post positions itself as pulling together several other people's independent framings of the same shift: Viv Trivedy's "Anatomy of an Agent Harness" writeup (credited with coining the term "harness engineering"), HumanLayer's framing of agent failures as configuration ("skill issue") problems, Anthropic's own published engineering guidance on designing harnesses for long-running work, and Birgitta Böckeler's account of what this looks like from a user's perspective. Author Addy Osmani presents the synthesis, including the Terminal Bench and "skill issue" observations, as drawn from these other sources rather than as his own original research finding.
