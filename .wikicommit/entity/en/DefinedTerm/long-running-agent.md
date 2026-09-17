---
title: "Long-running Agent"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An AI agent designed to keep making forward progress on a goal across many sessions and sandboxes, possibly over days or weeks, by persisting state outside the model's context window and handing off cleanly between sessions."
---

A long-running agent is an AI agent that keeps making progress on a goal across many context windows and sandboxes -- possibly over days or weeks -- rather than being structured around a single sitting. It can recover from failure, leave structured artifacts behind, and resume where it left off, which requires solving for persistence, recovery, and verification in a way a single chat-window agent does not need to.

## Usage

The term covers at least three distinct things that blur together in a real production agent. Long-horizon reasoning is a model-quality property: the ability to plan and execute over many dependent steps and recover from a wrong turn taken steps earlier. Long-running execution is a harness property: the agent's process itself runs for hours or days, possibly invoking the model thousands of times across the run. Persistent agency is an identity property: the agent outlives any single task, accumulating memory and learning preferences across sessions (the "Memory Bank" flavor of the concept).

Anthropic, Cursor, and Google are described as having converged on the same underlying shape for long-running execution specifically: separate the model loop from the execution sandbox from a durable session log, split planning from generation from evaluation, and treat compaction, hooks, and context resets as first-class rather than incidental (see [[DefinedTerm/brain-hands-session-split]], [[DefinedTerm/planner-worker-model]], [[DefinedTerm/ralph-loop]]).

## When It Applies

Three obstacles are named as the reason ordinary agent designs stop working at this scale: finite context (even a large window fills, and [[DefinedTerm/context-rot]] degrades performance before the hard limit is reached), no persistent state (a new session starts blank, so every session change is a productivity loss without an explicit handoff), and no self-verification (a model asked "are you done?" answers yes more often than it should). The suggested litmus test for whether the extra design effort is warranted is the longest uninterrupted unit of work the agent needs to perform: minutes do not need these patterns, but hours or days do.

## Related Terms

[[DefinedTerm/ralph-loop]], [[DefinedTerm/brain-hands-session-split]], [[DefinedTerm/checkpoint-and-resume]], [[DefinedTerm/planner-worker-model]], [[DefinedTerm/harness-engineering]], [[DefinedTerm/context-rot]]
