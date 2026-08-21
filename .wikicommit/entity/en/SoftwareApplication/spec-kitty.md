---
title: "Spec Kitty"
type: "schema:SoftwareApplication"
lang: en
tags: [spec-driven-development, git-worktree, code-review, agentic-coding, framework]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An open-source command-line tool for specification-driven development with code agents, which keeps specifications, plans and tasks inside the repository and isolates implementation work in git worktrees behind review and acceptance gates."
  applicationCategory: "DeveloperApplication"
  author: ""
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

Spec Kitty is an open-source command-line tool for [[DefinedTerm/spec-driven-development]] with code agents. It turns product requirements into repeatable workflows, keeping specifications, plans and tasks inside the repository itself in a dedicated directory, and using git worktrees to isolate implementation work. Its declared flow runs through the steps spec, plan, tasks, next, review, accept and merge, and it announces support for multiple agents including Claude, Cursor and Gemini.

## Overview

In the six-dimension taxonomy of [[ScholarlyArticle/from-prompt-to-process]], Spec Kitty covers specification, roles and validation, with its distinctive trait in execution. It scores 2, 1, 1, 2, 2, 1 across specification, context, roles, execution, validation and portability — a total of 9 out of 12, second-highest of the six frameworks examined, and the only one to score 2 on execution.

## Features

The worktrees are what set it apart in that assessment: they isolate work packages so agents can implement in a controlled way, with review and acceptance required before the merge. The paper reads this as inserting human control points into the flow and bringing agentic development closer to established code-review practice, and uses the same feature as its illustration that its taxonomy dimensions are overlapping lenses rather than partitions — worktree isolation is execution, while the required pre-merge review is validation.

## History

Its main recorded caveat is traction rather than design: the paper notes still-modest adoption compared with the other frameworks in its set, and says Spec Kitty was included at the threshold of its traction filter, leaving maturity and adoption open questions. Its dependence on its own repository conventions and on git worktrees is also given as the reason its portability is rated partial despite multi-agent support.
