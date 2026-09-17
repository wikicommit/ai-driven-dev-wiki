---
title: "Long-running Agents"
type: "schema:BlogPosting"
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
  description: "A survey of long-running AI agents -- agents that keep making progress across many sessions and sandboxes over hours, days, or weeks -- comparing how Anthropic, Cursor, and Google have each converged on separating the model loop, the execution sandbox, and a durable session log."
  author: "Addy Osmani"
  datePublished: "2026-04-28"
---

This post argues that the dominant "chat window with a loop in it" picture of an AI agent has a ceiling: the model forgets, declares work "complete" prematurely, and the whole interaction is structured around a single sitting. It sets out what comes after -- an agent that keeps making forward progress on a goal across many sessions and sandboxes, possibly for days or weeks, while leaving the workspace clean enough for the next session to pick up where the last left off -- and surveys how Anthropic, Cursor, and Google have each built for it.

The post distinguishes three things "long-running" gets used to mean (long-horizon reasoning, long-running execution, and persistent agency, see [[DefinedTerm/long-running-agent]]) and argues that production long-running agent designs are mostly answers to three recurring obstacles: a context window that eventually fills regardless of size, no state that survives a new session starting blank, and a model's unreliable self-report of whether it is actually done.

## Key Points

- The [[DefinedTerm/ralph-loop]], a bash-script-simple loop that picks an unfinished task, prompts the agent, runs checks, and appends state to files on disk, is presented as the practitioner-level version of the same idea every larger system builds on: state lives outside the agent's context, so each fresh iteration reads enough off the filesystem to keep going.
- Anthropic's two harness posts describe an initializer/coding-agent split for autonomous full-stack development, and then a [[DefinedTerm/brain-hands-session-split]] architecture behind [[SoftwareApplication/claude-managed-agents]], in which the model-and-harness loop, the sandboxed execution environment, and an append-only session event log are each independently replaceable; Anthropic reported time-to-first-token dropping roughly 60% at p50 and over 90% at p95 from decoupling them.
- Anthropic's separate scientific-computing post reduces the same pattern to `CLAUDE.md` as a living plan, `CHANGELOG.md` as portable lab notes, and a Ralph-loop `for` loop that kicks the agent back into context whenever it claims completion; its case study is a Boltzmann solver Claude Opus 4.6 built over a few days that reached sub-percent agreement with a reference implementation.
- Cursor's own account of scaling long-running coding agents describes working through three coordination designs -- flat file-locking, then optimistic concurrency control, then a hierarchy of Planners, Workers, and Judges (see [[DefinedTerm/planner-worker-model]]) -- and reports that a GPT model outperformed Opus specifically for extended autonomous work because Opus tended to stop early, so the same task can call for a different model in a different role.
- Google folded Vertex AI into the [[SoftwareApplication/gemini-enterprise-agent-platform]] at Cloud Next '26, productizing the same brain/hands/session shape as named services (Agent Runtime, Agent Sessions, Agent Memory Bank, Agent Sandbox, and others) with identity and audit-trail features bundled in.
- Osmani and Shubham Saboo's separately published "five patterns for long-running agents" names [[DefinedTerm/checkpoint-and-resume]], delegated approval (see [[DefinedTerm/human-in-the-loop]]), memory-layered context, ambient processing, and fleet orchestration as the patterns that separate working long-running agents from demos.
- The post's practical recommendations: write down the done-condition in an external file before the agent starts, separate the evaluator from the generator rather than letting a model grade its own work, invest in the session log rather than only the prompt, and treat compaction and full context resets as first-class rather than an afterthought.
- It names five unsolved problems as of this writing: cost (an unbudgeted 24-hour run can burn through a week's API spend), security (a larger attack surface from API keys, cloud access, and shell execution), alignment drift (re-summarization losing fidelity to the original goal over many context windows), verification (auditing a day of autonomous activity is a real human-time cost), and the human role, which the post frames as shifting from writing code to writing specs precise enough for an autonomous executor to run on for a day.

## Context

The post positions Google, Anthropic, and Cursor as having converged on the same underlying shape -- separating the model loop from the execution sandbox from the durable session log, and splitting planning from generation from evaluation -- while differing in surface area: Google's platform bundles identity and audit trails at enterprise scale, Claude Managed Agents is "Anthropic's harness, hosted," and Cursor's background agents pull long-running coding out of the IDE and into the cloud. Osmani presents it as a follow-up to his own earlier posts on harness primitives ([[BlogPosting/agent-harness-engineering]]) and the Ralph loop ([[BlogPosting/self-improving-agents]]), and attributes each vendor's specific claims and case studies to that vendor's own published posts rather than to his own testing.
