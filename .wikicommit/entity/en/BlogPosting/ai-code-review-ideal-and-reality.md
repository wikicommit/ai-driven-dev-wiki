---
title: "AIコードレビューの理想と現実 ─ Devinをチームに導入して気づいたこと"
type: "schema:BlogPosting"
lang: en
tags: [agentic-code-review, coding-tools, ci-cd, agent-config]
sources:
  - type: url
    url: 'https://tech-blog.yayoi-kk.co.jp/entry/2026/02/18/110000'
    hash: sha256:f257dca18ea047972a127fe941a248ac2184ccbbb5bd4fc88d619fb52132227a
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A Yayoi engineer's account of running Devin as a routine code reviewer: review perspectives standardized in a committed prompt file, review sessions opened automatically from GitHub Actions, and AGENTS.md supplying project context. It is as much about the limits found in practice as the gains."
  author: "Sekiguchi (y_redamoon)"
  datePublished: "2026-02-18"
  publisher: "Yayoi Co., Ltd."
---

This post is a practitioner's report from a team at Yayoi that has made [[SoftwareApplication/devin]] a routine part of its code review, rather than an evaluation or a product announcement. Most of its detail concerns two artifacts committed to the repository alongside the agent — a file of review perspectives and a file of project context — and it closes by naming the parts of review the author considers unsuited to delegation.

The author gives five problems the team was trying to relieve: review effort growing, reviewer load, the psychological cost on both sides when people exchange fine-grained criticism, difficulty standardizing what gets looked at, and small issues being missed. Notably the third is stated as a problem of human-to-human review specifically.

The account is explicitly mid-flight. The sections on continuous prompt tuning, accumulating knowledge of false-positive patterns, CI tuning and periodic retrospectives are written as the direction the team intends to take, with the author noting the setup is still being built out — not as measured outcomes.

## Key Points

- Review perspectives are standardized by committing them to `.github/devin-review-prompt.md` in the repository, organized as seven groups: code quality, architecture and design, security, performance, tests, documentation, and project-specific requirements. The author's stated reason for keeping it in the repository is that CI/CD can read it from there and team members can share it easily.
- The author singles out the project-specific group twice, in the benefits about standardization and about catching small issues, as the one that gets checked without omission. It holds rules particular to the project: that logging must use the team's OpenTelemetry-format logger rather than `console.log()`, that branches follow `features/{ticket-number}[/task-name]`, that PR titles carry a `feat:`/`fix:`/`hotfix:` prefix, and that particular design documents must be updated when the database, API or infrastructure changes.
- Review runs from GitHub Actions on pull request `opened`, `synchronize` and `reopened`. The workflow collects the PR's changed files, reads the review-perspective file, extracts a prompt template delimited in `AGENTS.md`, and creates a session against the Devin API; Devin posts its findings back as comments on the PR.
- Two workflow conditions are given as the means of keeping cost and noise down rather than as incidental configuration: forked and draft PRs are excluded, and a concurrency group with `cancel-in-progress` ensures only the latest push to a PR is reviewed.
- The team relies on [[DefinedTerm/agents-md]] being read by Devin automatically, and uses it to carry setup commands, code style and test guidelines, project structure, development workflow and Devin-specific notes. This is the author's account of Devin's behavior, not a specification claim.
- Output is requested in a fixed shape — findings grouped by priority, each with a concrete suggested fix, plus a "good points" section — and the author credits the fixed shape, rather than the findings themselves, for making results quick to work through.
- A low-precision AI reviewer is described as actively counterproductive: noise accumulates until developers stop reading review comments at all. The author presents continuous prompt adjustment and accumulated knowledge as prerequisites for the practice rather than refinements of it.
- AI review is said to get in the way when speed matters — immediately before a release, or on a hotfix — and the author names concurrency settings and a label-based skip as the operational answers.
- Response latency was poor at first and improved as the agent accumulated project context; the author reports first sessions remaining slow regardless. This is one team's observation, not a measured benchmark.
- The post reserves specific work for humans: deciding whether a review passes, articulating why, and explaining design decisions to stakeholders outside engineering. It also argues that recording the reasoning behind a pass-or-fail decision on the PR is itself worth doing, as a way of accumulating shared understanding.

## Context

The post sits alongside this wiki's other firsthand accounts of [[DefinedTerm/agentic-code-review]]. What distinguishes this team's approach is where the engineering effort goes: not into the agent's architecture, but into narrowing and committing the two files a single agent reads.

The author is clear about the perspective's limits. The team's own experience is the only evidence offered, no precision figures are given, and the improvement measures are stated as intentions. A separate observation the post makes about review culture — that phrasing varies between human reviewers in ways that add avoidable friction, and that a uniform format may help — is offered as a hypothesis about an expected effect rather than something the team has measured.

The author also notes a newer Devin Review feature, described as a web-based code review platform, and states the team's intention to compare it against the API-driven approach used here; no comparison results are reported.
