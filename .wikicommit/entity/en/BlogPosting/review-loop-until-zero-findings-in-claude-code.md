---
title: "Claude Codeで\"指摘ゼロになるまで回すレビューループ\"を組んだが、ゼロにならなかった"
type: "schema:BlogPosting"
lang: en
tags: [agentic-code-review, claude-code, multi-agent, agent-failure-modes]
sources:
  - type: url
    url: 'https://zenn.dev/pepabo/articles/claude-code-review-loop-zero-findings'
    hash: sha256:d0532ff50aac8dbea50293dd13e8a3a76ebf8413805792d29a131945fbe53bfe
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A March 2026 Japanese-language post on GMO Pepabo's Zenn publication describing an AI code review built in Claude Code from six specialised reviewers run in parallel, a validation agent that filters their findings, and an auto-fix loop meant to run until no findings remained — which never reached zero."
  author: ["atani"]
  datePublished: "2026-03-24"
  publisher: "GMO Pepabo"
---

This Japanese-language post, published on GMO Pepabo's Zenn publication, describes an AI code review its
author built with [[SoftwareApplication/claude-code]] to relieve a growing queue of pull requests awaiting
review. The design splits review across specialised reviewers run in parallel and loops automatic fixes and
re-reviews with the aim of reaching zero findings. As the title says, the loop never reached zero; the author
writes that the reasons it did not were the more useful lesson.

## Key Points

- The author found that asking one AI to "look at everything" produced shallow findings, and split review
  across six reviewers with narrowed roles — code (logic, edge cases, error handling), security, tests, DDD,
  readable code, and spec/design — on the view that, as with human reviewers, a narrowed role draws deeper
  findings.
- The code reviewer is told to act as a mentor rather than a gatekeeper, and findings are graded Must Fix,
  Should Fix, Consider or Nitpick.
- The reviewers are started in parallel as background agents through Claude Code's Agent tool; the PR diff is
  classified into backend, frontend, test and config files and each reviewer receives only the relevant files.
- The convergence loop merges the six results, validates each finding, automatically fixes critical and
  warning findings, re-reviews, and ends when no findings remain or after five rounds.
- The author says the loop can run away — a fix draws a new finding from another AI, whose fix draws another —
  and describes safety valves: minimal fixes limited to what was flagged, no fixes for findings that need a
  design decision (those are reported to a human), at most three retries on test failures, stopping when the
  scope exceeds 20 files, and a forced stop at five rounds with the remaining findings reported. Designing the
  line between what is fixed automatically and what goes back to a human was, the author says, the hardest part.
- A separate Claude Code agent validates the reviewers' findings against the codebase's context and deletes or
  downgrades to info those it judges invalid. The author cautions that it can wrongly reject valid findings and
  that agreement between AIs does not make a judgment correct, and uses it only as a filter that works to some
  degree.
- Across a few dozen PRs, the author's rough impression was about 40% useful findings, 30% noise from not
  knowing project conventions (about half removed by the validation agent), 20% off-target findings from
  missing context (recurring patterns were added to the prompts as exclusions), and 10% unexpected discoveries,
  such as design contradictions or inconsistencies with past reverts, which the author valued most.
- A CI version runs three headless agents (code, security, test) in parallel with `claude -p` when a PR is
  opened and aggregates their results as JSON.
- The author concludes that AI review replaced checklist-style review but not interactive review: mechanical
  checks no longer need human comments, while judging design, fit with business requirements and a PR's intent
  remain human work. With E2E test results and screenshots also attached to PRs, the team reports that it
  matched the previous year's merge count within two and a half months of adopting the setup.

## Context

This is one practitioner's report on their own team's system, and its figures for finding quality are stated as
the author's rough impression. It is one of several accounts of the same failure shape collected under
[[DefinedTerm/review-loop-non-convergence]].
