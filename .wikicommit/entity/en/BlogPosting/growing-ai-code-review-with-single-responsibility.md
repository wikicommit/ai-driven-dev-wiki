---
title: "AIコードレビューを「単一責任の原則」で育てた話"
type: "schema:BlogPosting"
lang: en
tags: [code-review, agents, agent-config]
sources:
  - type: url
    url: 'https://zenn.dev/globis/articles/d0c73d2b176ba5'
    hash: sha256:d007e48e9860eef6953063dd12b23e8be1cf1576ddabcc4574d8a292c21d4357
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A DevEx team's account of why its general-purpose AI code reviewer was being ignored, and of splitting it into many single-concern review agents — applying the single responsibility principle to the reviewer itself — with past production failures fed back in as accumulated knowledge."
  author: "emi084"
  datePublished: "2026-03-17"
  publisher: "GLOBIS Tech"
---

This post is a practitioner account of an AI code review deployment that was failing for a specific
reason and of the change that fixed it. The team had been running review through
[[SoftwareApplication/claude-code]] since around spring 2025, having adopted it because human review
kept missing the same concerns; what went wrong was that a reviewer configured only in general terms
lacked the context to say anything pointed, and enough off-target comments accumulated that team
members began ignoring its output altogether.

The response the post describes is to apply the single responsibility principle to the reviewer: one
agent per review concern, each with a narrow context, rather than one agent asked to review
everything. The post presents this as the design idea worth carrying across tools, and is explicit
that the specific agents are internal and that the transferable part is the shape rather than the
contents.

It is one team's firsthand report, and its evidence for the approach working is its own experience
rather than a measurement.

## Key Points

- Off-target review comments are not a neutral cost: the post reports that once enough of them
  accumulated, team members started ignoring the AI reviewer entirely, which is a failure of the
  whole deployment rather than a quality shortfall in individual comments.
- The fix offered is to split the reviewer by concern, one agent per review dimension, on the
  grounds that a general-purpose configuration does not carry enough context to review any one
  dimension well. The post frames this explicitly as the single responsibility principle applied to
  an AI agent.
- Agents are defined as Markdown files with YAML front matter — a name, a `description` and a model
  setting in the front matter, a system prompt in the body — and grouped into plugins, one for the
  team's Rails-specific reviewers and one for reviewers that do not depend on the stack.
- Dispatch needs no separate trigger configuration: the post states that the orchestrating agent
  reads each sub-agent's `description` field and selects one from it, so writing that description
  concretely — which files it applies to, what it looks for — is what makes invocation reliable. An
  abstract description is given as the cause of both missed and spurious invocations.
- The post reports having the AI write each agent's `description` from its system prompt, while
  noting that whether it is then actually invoked as intended is a separate question: a clear
  file-pattern trigger is easy for the model to judge, and where there is none, the team creates
  test pull requests to confirm the behaviour.
- Knowledge accumulates by a deliberate loop rather than by tuning: when a flaky test is fixed and
  the team judges the pattern likely to recur elsewhere, the detection pattern is added to the
  reviewer, so fixing the failure and growing the agent are the same act.
- The post argues the approach does not depend on the tool, naming Cursor rule files and GitHub
  Copilot's instructions file as places the same role-splitting could be expressed, and states that
  what matters is narrowing each reviewer's context.
- A closing claim is that writing rules down for an AI reviewer has a second payoff independent of
  the review: it converts a team's tacit knowledge into explicit form that stays with the team.

## Context

The post places the change against two alternatives the team had already tried. Checklists were used
first and are reported as high-effort and still leaky. For the flaky-test concern specifically, a
custom static-analysis rule was attempted before the agent and abandoned because the patterns were
too complex to express that way — which is the post's argument for why an LLM reviewer is the right
tool for that particular class of defect rather than a lint rule.

The author also notes that an official code review feature shipped in March 2026 for the tool the
team uses, and that the team costed it and did not switch, continuing with what it had built.
