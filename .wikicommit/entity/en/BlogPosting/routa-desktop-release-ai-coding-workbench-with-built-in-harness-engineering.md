---
title: "Routa 桌面版发布：内建 Harness 工程的 AI Coding 研发协作工作台"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, multi-agent, coding-agents, quality-gates]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/routa-harness-engineering-builtin-platform/'
    hash: sha256:4ba80d8b7c39b0795402b9a0c3ede0acef5af2849700b26983a9c5d2c5201060
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An April 2026 Chinese-language blog post by Phodal Huang announcing the desktop release of Routa, which he presents as an AI coding collaboration workbench built on the formula \"Harness engineering + Coding Agent + Kanban\". It describes Kanban columns as quality gates, a relay of lane-specialist agents, and harness engineering as part of the definition of done."
  author: ["Phodal Huang"]
  datePublished: "2026-04-14"
---

This post, written in Chinese by Phodal Huang, announces the desktop release of
[[SoftwareApplication/routa]] and explains the thinking behind it. The author says that his work on the
ACP protocol and multi-agent collaboration convinced him that a single coding agent is no longer the key
problem; what matters is getting several agents to work together inside one engineering system. After a
series of multi-agent experiments and a growing body of thinking about harness engineering, he arrived
at a formula — "Harness engineering + Coding Agent + Kanban = an AI automated R&D workbench" — and
presents Routa as the first fairly complete product embodiment of it.

The post's recurring question is what "done" means. The author argues that a chat session can carry
one act of generation but not a long-lived flow of tasks, in which requirements are split, stages
advance, different roles take over, and results are verified, sent back and retried before only some
of them pass the gates into delivery.

## Key Points

- The author says the hardest problem his team met in moving from agent teams to Kanban was the
  definition of done (DoD). In a spec-based mode, DoD means development is complete — the spec's
  acceptance criteria are met; in a Kanban mode, it means delivery is complete — the card is ready to
  enter the `done` column. In his words, "done" in the spec mode is only "dev done" in Kanban, with
  verification, gates, evidence and state transitions still in between.
- Once DoD means delivery, he argues, Kanban becomes a task-level protocol: moving a card to another
  column is a state switch that redefines its required inputs, outputs, verification and next actions,
  so the columns act as entry and exit gates rather than a visual queue. Each downstream stage first
  checks that the upstream stage delivered what it owed and sends the card back if not.
- Multi-agent work, in his view, is not a parallelism problem: more agents with unclear
  responsibilities and handoffs only produce noise faster. He argues for clarity over quantity — a
  relay chain of lane specialists, each doing only its own column's work, verifying the upstream
  output first and explicitly handing responsibility downstream, with gates, rollback and recovery.
- He says that for a codebase AI agents keep rewriting, a team must decide in advance which module
  boundaries cannot be broken, which contracts must stay stable, which checks are mandatory before
  merging, which regressions must be caught before release, and how progressive disclosure keeps the
  code understandable to agents. At that point, he writes, the harness has entered the definition of
  done itself, moving architecture fitness, gate rules, evidence requirements and release conditions
  forward so the system can decide whether a result moves on or stops.
- He distinguishes a technical "done" — the delivered code has passed every quality gate and can be
  merged — from a business "done" — the delivered code meets all acceptance criteria and can be
  released to production.
- He summarises the formula's division of labour as coding agents supplying execution, Kanban supplying
  task state, and harness engineering supplying constraints, verification and the definition of done,
  and says Routa aims to reconnect the flows of tasks, responsibilities and evidence rather than to be
  a chat-style coding agent or merely a multi-agent container.

## Context

The post is a product announcement by the project's author, framed by his own earlier experiments and
writing on multi-agent coding, which it links; it describes the design and reports no evaluation
results. It applies the author's thinking on [[DefinedTerm/harness-engineering]] to task flow and
the definition of done.
