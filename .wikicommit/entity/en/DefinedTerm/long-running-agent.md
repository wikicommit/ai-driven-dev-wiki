---
title: "Long-running Agent"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  - type: url
    url: 'https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf'
    hash: sha256:c63d41952636629543bbc11004c9be52b96f346284383c32bcd91f9130d25932
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
    hash: sha256:26ce4c203cbb030f31253f1eb174b46b2c0203c9b44576aa4654b89b4d7be777
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An AI agent designed to keep making forward progress on a goal across many sessions and sandboxes, possibly over days or weeks, by persisting state outside the model's context window and handing off cleanly between sessions."
---

A long-running agent is an AI agent that keeps making progress on a goal across many context windows and sandboxes -- possibly over days or weeks -- rather than being structured around a single sitting. It can recover from failure, leave structured artifacts behind, and resume where it left off, which requires solving for persistence, recovery, and verification in a way a single chat-window agent does not need to.

## Usage

The term covers at least three distinct things that blur together in a real production agent. Long-horizon reasoning is a model-quality property: the ability to plan and execute over many dependent steps and recover from a wrong turn taken steps earlier. Long-running execution is a harness property: the agent's process itself runs for hours or days, possibly invoking the model thousands of times across the run. Persistent agency is an identity property: the agent outlives any single task, accumulating memory and learning preferences across sessions (the "Memory Bank" flavor of the concept).

Anthropic, Cursor, and Google are described as having converged on the same underlying shape for long-running execution specifically: separate the model loop from the execution sandbox from a durable session log, split planning from generation from evaluation, and treat compaction, hooks, and context resets as first-class rather than incidental (see [[DefinedTerm/brain-hands-session-split]], [[DefinedTerm/planner-worker-model]], [[DefinedTerm/ralph-loop]]).

Anthropic's own account in [[BlogPosting/effective-harnesses-for-long-running-agents]] narrows the
problem to one sentence — agents work in discrete sessions, and each new session begins with no
memory of what came before — and gives it the image of a project staffed by engineers working shifts
where each arrival remembers nothing of the last. Its contribution is a concrete harness rather than
a taxonomy. Two failure modes are reported from running a frontier model in a loop against a
high-level prompt: the agent attempts to one-shot the whole application and exhausts its context
mid-feature, leaving the next session to reconstruct what happened; and, once some progress exists, a
later session sees it, concludes the job is done, and stops.

The described remedy splits the run in two. An [[DefinedTerm/initializer-agent]] runs once and builds
the environment every later session depends on — a startup script, a progress log, an initial commit,
and a JSON list of every feature the prompt implies, each marked failing. Every session after it reads
that state, advances exactly one feature, verifies it end-to-end, and leaves the repository committed
and documented. The stated key insight is that what a fresh context window needs most is a fast way to
understand the state of the work, supplied by the progress file alongside the git history, and the post
notes the practices were modelled on what effective software engineers do daily.

## When It Applies

Three obstacles are named as the reason ordinary agent designs stop working at this scale: finite context (even a large window fills, and [[DefinedTerm/context-rot]] degrades performance before the hard limit is reached), no persistent state (a new session starts blank, so every session change is a productivity loss without an explicit handoff), and no self-verification (a model asked "are you done?" answers yes more often than it should). The suggested litmus test for whether the extra design effort is warranted is the longest uninterrupted unit of work the agent needs to perform: minutes do not need these patterns, but hours or days do.

[[TechArticle/2026-agentic-coding-trends-report]] describes the same category as a trajectory rather
than a design problem, and puts numbers on where it had reached. It characterises early agents as
handling one-shot tasks of a few minutes — fix this bug, write this function, generate this test —
with agents producing full feature sets over several hours by late 2025, and predicts agents working
for days at a time in 2026, building entire applications with human involvement concentrated at
strategic decision points. Its reported example of the state of the art is a single autonomous run of
seven hours implementing an activation-vector extraction method in vLLM, a 12.5-million-line
multi-language codebase, which the report says reached 99.9% numerical accuracy against the
reference method. The report's argument for why the horizon matters is economic rather than
technical: when an agent can work unattended for long periods, projects that were never worth
staffing become feasible, and backlogs of technical debt that accumulated because no one had time
for them can be worked through systematically.

## Related Terms

[[DefinedTerm/ralph-loop]], [[DefinedTerm/brain-hands-session-split]], [[DefinedTerm/checkpoint-and-resume]], [[DefinedTerm/planner-worker-model]], [[DefinedTerm/harness-engineering]], [[DefinedTerm/context-rot]], [[DefinedTerm/initializer-agent]]
