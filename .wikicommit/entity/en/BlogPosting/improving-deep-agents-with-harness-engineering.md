---
title: "Improving Deep Agents with harness engineering"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, agent-evaluation, agentic-coding, agent-architecture]
sources:
  - type: url
    url: 'https://blog.langchain.com/improving-deep-agents-with-harness-engineering/'
    hash: sha256:7628e7920b4c219963d45c07cb27a6039a14ef5a60f3939b0ccb424dd7481ddd
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A LangChain blog post reporting how the company raised its coding agent's Terminal Bench 2.0 score by changing only the harness around a fixed model, and the harness changes — self-verification, injected environment context, loop detection and reasoning budgeting — that it credits for the gain."
  author: ["Vivek Trivedy"]
  datePublished: "2026-02-17"
  publisher: "LangChain"
---

This post by Vivek Trivedy on LangChain's blog is a report on applying
[[DefinedTerm/harness-engineering]] to LangChain's own coding agent, deepagents-cli, which the post links to within the
[[SoftwareApplication/deep-agents]] repository. Its headline is that the agent went from just outside the Top 30 to
the Top 5 on Terminal Bench 2.0 ([[Dataset/terminal-bench]]) while the model, `gpt-5.2-codex`, was held
fixed and only the harness changed — a gain of 13.7 points, from 52.8 to 66.5.

The post frames a harness as the system built around a model to mold its "inherently spiky
intelligence" toward the tasks one cares about, optimizing for goals such as task performance, token
efficiency and latency. Of the many knobs a harness offers, the team deliberately restricted itself to
three — the system prompt, tools, and middleware, LangChain's term for hooks around model and tool
calls — and used traces of the agent's runs to decide what to change.

## Key Points

- The experiments ran on Terminal Bench 2.0, which the post describes as a now-standard benchmark for
  agentic coding with 89 tasks across domains such as machine learning, debugging and biology; runs
  were orchestrated with Harbor in Daytona sandboxes, and every agent action was stored in LangSmith.
- Trace analysis was made repeatable by packaging it as an Agent Skill: fetch experiment traces, spawn
  parallel error-analysis agents whose findings a main agent synthesizes, then make targeted harness
  changes. The post likens this to boosting, and says a human can help — though is not required — in
  checking proposed changes, since changes that overfit to one task can cause regressions elsewhere.
- The most common failure it reports was an agent that wrote a solution, re-read its own code, judged it
  fine and stopped without testing. Its remedy was system-prompt guidance for a plan, build, verify and
  fix cycle (see [[DefinedTerm/verification-loop]]), plus a `PreCompletionChecklistMiddleware` that
  intercepts the agent before it exits and reminds it to verify against the task specification — which
  the post compares to the [[DefinedTerm/ralph-loop]].
- A `LocalContextMiddleware` maps the working directory and its parents and children and finds tools
  such as Python installations when the agent starts; the post argues that injecting this context
  reduces the error surface of context discovery and search, and calls this onboarding the agent into
  its environment.
- The team also prompted the agent to write code that programmatic tests will measure, and injected
  time-budget warnings to nudge it toward finishing and verifying, on the grounds that agents are bad at
  estimating time.
- A `LoopDetectionMiddleware` tracks per-file edit counts and, after a set number of edits to the same
  file, suggests reconsidering the approach, against [[DefinedTerm/doom-loop]]s. The post calls this a
  heuristic engineered around today's perceived model issues, likely to become unnecessary as models
  improve.
- On reasoning compute, it reports that running only at the highest reasoning setting (`xhigh`) scored
  53.9% because of agent timeouts, against 63.6% at `high`, and adopted a
  [[DefinedTerm/reasoning-sandwich]] — `xhigh` for planning, `high` for implementation, `xhigh` for
  verification — as its baseline.
- Its practical takeaways are to do [[DefinedTerm/context-engineering]] on the agent's behalf, push
  agents to self-verify, use traces as a feedback signal, detect and fix bad patterns in the short term,
  and tailor harnesses to models. On the last point it reports that an earlier harness version run with
  Claude Opus 4.6 scored 59.6%, which it attributes to not having run the same improvement loop with
  Claude.

## Context

The post is LangChain reporting results for its own open-source agent on a public benchmark; the
figures are the team's own measurements and the harness heuristics are presented as findings from its
experiments rather than as general rules. It closes by naming open research directions — multi-model
systems, memory primitives for continual learning, and measuring harness changes across models — and
says the team published a dataset of its traces.
