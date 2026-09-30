---
title: "Practical Loop Engineering"
type: "schema:BlogPosting"
lang: en
tags: [agents, loop-engineering, agentic-engineering]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/practical-loop-engineering/'
    hash: sha256:2771ce50f0195e96533a1b4ed0d2ab482f6206ca955131432f4b25483dd4a818
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A practitioner's account of how he applies loop engineering day to day with Claude Code's /goal and /loop primitives: what each is for, how to combine them, separating the agent that makes a change from the one that checks it, what to delegate versus watch, and which tasks loops do not suit."
  author: ["Addy Osmani"]
  datePublished: "2026-08-14"
---

This post is a hands-on follow-up to the author's earlier writing on [[DefinedTerm/loop-engineering]] ([[BlogPosting/loop-engineering]]), describing how he actually uses it while running roughly five to ten agents in parallel. It defines a loop as an autonomous, self-correcting feedback cycle in which an agent repeatedly acts, tests its results and adjusts its approach until a specific goal is met, and centres on two primitives now built into [[SoftwareApplication/claude-code]]: `/goal`, which drives a single bounded task until a measurable finish line is reached, and `/loop`, which re-runs a prompt on a timer or fixed interval, much like a cron job.

The author contrasts this with the period before such primitives existed, when loop engineering meant hand-rolled bash loops and experiments such as the [[DefinedTerm/ralph-loop]], mostly on personal projects where hitting a wall cost little. He says he can now largely rely on the output of the primitives in Claude Code and Codex, but that a loop left alone without a well-defined end goal and constraints can leave a codebase in a problematic state, which is why the calculus calls for nuance between an evergreen codebase without users or much historical complexity and, say, a brownfield bank codebase. The post also quotes at length the Claude Code team's own classification of loops into turn-based, goal-based, time-based and proactive kinds.

## Key Points

- `/goal` is presented as suited to building a specific piece of work until it is provably done; the post recommends deterministic, verifiable completion criteria (for example a Lighthouse score threshold plus a turn limit) and being specific about which tooling measures them.
- The evaluator behind `/goal` is described as not a quality checker: according to the author it only examines the conversation transcript to see whether the hard rules specified have been met, not whether the content is good.
- `/loop` is described as a scheduler for polling logs, monitoring external state or repeating a task on a cadence; the two can be combined by using `/loop` to schedule a check and `/goal` to solve whatever it finds, though the author notes `/goal` has limits on how much can be packed into it.
- The author's rule of thumb for delegation: safer tasks (writing documentation for a finished feature, checking test coverage) can be delegated fully, while complex work, or anything touching authentication, security, finance or access to a system, is watched closely — this rests on his own practice.
- He argues the agent that did the work should not decide the work is good: one sub-agent drafts a change and a separate one verifies it, since a confident agent can evaluate only one dimension of a problem (desktop but not mobile performance, in his example).
- From a near-miss in which he almost pushed agent-written changes he had not read closely, he draws the lesson that one can delegate the task without delegating taste and judgment, and should check the result against one's own bar.
- His daily example is PR and issue triage on his open-source Agent Skills repository, where a scheduled loop reviews new items and closes those that clearly conflict with written contribution guidelines (such as a rule that translations are not accepted), shrinking the batch left for humans to review.
- Loops are described as a poor fit when "done" cannot be stated clearly — tasks needing human taste, subjective design or open-ended creative exploration — and a loop re-running the same command with no change in result is given as a sign it is spinning in place.
- Per the post, recurring loops expire seven days after creation and are session-scoped (resuming the session brings back any still inside that window); work that must outlive the session is moved to the cloud with `/schedule`.

## Context

The post builds directly on the Claude Code team's published framing of loops, which it summarises and quotes rather than originates, and on the author's earlier post on the same practice. He writes from his own experience as a heavy user of these tools, and several of the specifics — the seven-day expiry, session scoping, and the behaviour of the `/goal` evaluator — describe a single vendor's product at the time of writing. The author bio at the end of the post describes him as a Member of Technical Staff at Anthropic working on Claude Code, so the product it describes is his employer's.
