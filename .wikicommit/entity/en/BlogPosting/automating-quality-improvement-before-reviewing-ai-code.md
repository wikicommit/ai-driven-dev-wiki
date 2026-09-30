---
title: "AIによる実装の品質が微妙で毎回自分で指摘しまくる必要があったので、確認前に自動で品質を上げさせるようにした"
type: "schema:BlogPosting"
lang: en
tags: [agentic-code-review, claude-code, subagents]
sources:
  - type: url
    url: 'https://blog.shibayu36.org/entry/2026/03/23/173000'
    hash: sha256:a771a79f6b890d1b759e457b829a20cc2db5260f647ffb876954cae0a72fb4e7
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A developer's account of a Claude Code slash command, /self-review, that runs three differently focused reviewer agents in parallel after an implementation and then has a separate skill critically judge each finding, fixing only the valid ones and giving reasons for the rest, so that code quality is raised before the developer reads it."
  author: ["shiba_yu36"]
  datePublished: "2026-03-23"
---

The post (its title translates roughly as "AI's implementation quality was mediocre and I had to point
things out every time, so I made it raise the quality automatically before I check") describes a
personal workflow for [[SoftwareApplication/claude-code]]. The author reports that although Claude Code
could implement changes in one go, the resulting code often fell short of the author's own standards,
even when the design had been worked out beforehand in plan mode, so every change ended up needing the
author's own comments.

The author's first attempt — having a subagent or Codex CLI review the code and fix everything before
checking it — ran into a different problem: AI review findings include off-target and excessive ones, and
having all of them addressed sometimes left the code messier. The fix the author adopted, credited to an
article by another developer, kawarimidoll, was to have the AI judge whether each finding is appropriate
before acting on it. The result is a `/self-review` slash command that chains a parallel review with a
critical evaluation step, which the author reports running after almost every implementation, before
reading the code.

## Key Points

- `/self-review` launches three reviewer agents in parallel: a general reviewer covering quality,
  security and performance; a `codex-reviewer` that uses Codex CLI's `codex review` command, valued by
  the author for giving the perspective of a model other than Claude; and a `simplify-reviewer` focused on
  readability, consistency and maintainability, aimed at the over-abstraction and unnecessary complexity
  the author associates with AI-generated code.
- The general reviewer is based on the reviewer agent in kawarimidoll's article, and the
  simplify-reviewer on Anthropic's official code-simplifier agent.
- Overlapping findings between the three reviewers are not treated as a problem: when several reviewers
  flag the same place, the author reads that as a sign the finding has higher priority.
- After all reviews finish, a `/fix-review-comments` skill evaluates each finding critically — asking
  whether it really needs fixing — fixes only the ones it judges valid, and gives a reason for each one it
  declines. This step is the one the author identifies as the key to the setup, and it too is modelled
  on a command from kawarimidoll's configuration.
- In the example session shown, the three reviewers raised ten findings in total, of which six were
  addressed and four declined; the addressed ones appear as five items because one covers a point two
  reviewers shared. Each declined finding carries a reason such as "intentionally designed that way in
  the requirements" or "already covered by the existing text". The author says this project-aware
  selection is what makes it possible to leave the fixes to run automatically.
- The claimed outcome is that the quality of the code is raised to some extent before the author reads
  it; this rests on the author's own experience, and the post reports no measurement.

## Context

The post is a single developer's firsthand account of a personal configuration, published in a public
repository of configuration files. It sits alongside other writing on AI reviewing AI-generated code
before a human does (see also [[DefinedTerm/critical-dialogue-review]]). The distinguishing idea here —
critically triaging review findings before fixing them rather than applying all of them — is described
on [[DefinedTerm/review-finding-triage]].
