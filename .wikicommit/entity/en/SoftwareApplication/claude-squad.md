---
title: "Claude Squad"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/future-agentic-coding/'
    hash: sha256:b6fa751c05fa1595dabeb21c14458cf4c51a1dd2997ce1edb3920fd3cebddf4a
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source terminal application that multiplexes Claude, spawning several Claude Code instances that work concurrently in separate tmux panes so a developer can give each one a different task."
  applicationCategory: "Multi-agent orchestration tool"
---

Claude Squad is an open-source terminal application that multiplexes Anthropic's Claude: it spawns several [[SoftwareApplication/claude-code]] instances working concurrently in separate tmux panes, so a developer can hand each one a different task. [[BlogPosting/future-of-agentic-coding-conductors-to-orchestrators]], which describes it as popular, groups it with [[SoftwareApplication/conductor]] as an example of tooling built for running a set of coding agents in parallel rather than one at a time.

## Capabilities

The mechanism is terminal multiplexing rather than a hosted service: the instances run locally, each in its own tmux pane, and the developer assigns work to each separately. The stated payoff is parallelism — the post's phrasing is that this lets a developer code "10x faster" by parallelizing, which is that post's characterization rather than a measured figure.
