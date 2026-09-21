---
title: "Claude Code Action"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, agents, ci, coding-tools]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60882/'
    hash: sha256:7997cccac08ed6a2731d85a3012e81cea6de4b141192497c171f97de0740feb1
  - type: url
    url: 'https://developersblog.dmm.com/entry/2025/12/02/110000'
    hash: sha256:fd805ea09ceea62557093852cd7e6e52043a461198208dca231e0465b7254161
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A GitHub Action that runs a Claude Code agent against a pull request, so review, CI-failure diagnosis and follow-up work can happen on the PR page itself. Its review flow is scriptable, which two teams used to build review and auto-approval flows of their own."
  applicationCategory: "AI code review"
  featureList: "Runs a Claude Code agent on GitHub pull requests; scriptable multi-phase review flows with subagents; scriptable scoring and auto-approval of pull requests; CI-failure diagnosis and fixing from the PR; responding to review comments and opening follow-up PRs"
  author: "[[Organization/anthropic]]"
---

Claude Code Action is a GitHub Action that puts a [[SoftwareApplication/claude-code]] agent on a pull request. [[BlogPosting/redesigning-code-review-for-the-ai-era]] describes a team adopting it for a specific reason: its members already spent their day on the GitHub PR screen checking comments and CI status, and the post's thought was that being able to carry code review through on that same screen would be considerably more efficient.

The property that post treats as decisive is how far the review flow can be shaped: it rates the freedom to customize as considerable, and in its comparison of three tools rates this one's customizability "unlimited" against "high" for [[SoftwareApplication/greptile]] — which it credits with auto-learned custom rules — and "medium" for GitHub Copilot. Rather than tuning a fixed review, the team wrote its own flow and had the action run it.

## Capabilities

- Runs a Claude Code agent against a pull request, where it can be used for code review, for diagnosing and fixing CI failures, and for acting on review comments including opening a new pull request from them.
- Review flows are scriptable as multiple phases with subagents assigned to separate concerns. The flow the post's team built, modelled on Claude's own published code-review example, runs four: a preparation phase gathering PR metadata, the issue being solved, the author, the development area and the guidelines applying to it; a review phase with one subagent per review perspective working against those guidelines; a severity-evaluation phase whose subagent judges whether each AI comment is valid, not fabricated, and how serious it is; and a posting phase that inline-comments only the high-severity findings, sends a summary, and suppresses anything another agent has already said.
- The same scriptability extends to approval rather than commentary. A second team, at DMM, used the action to build a mechanism that has the AI score a pull request and approve it automatically when the scores clear a threshold: its reviewer prompt scores four axes — `pr_clarity_score`, `code_quality_score`, `test_quality_score` and `security_quality_score` — and emits an object setting `auto_approval` to `"Y"` when the criteria are met, alongside a summary of the pull request and a stated reason. That team reports the accuracy as not bad and says prompt adjustment achieved stable operation ([[BlogPosting/what-ai-taught-us-about-code-review]]).
- Rated in the first post as the strongest of the three tools compared on domain understanding, and high on review quality; deep codebase understanding is listed among its characteristic features rather than scored against the others.
- Its reported drawbacks: setup is rated fiddly, which that post attributes to needing care around permissions, and it is the slowest of the three to review. The post also notes that deciding between an API key and a personal token is difficult on the Enterprise edition.

## Adoption & Ecosystem

The first post's team runs it as one of three AI reviewers alongside GitHub Copilot and [[SoftwareApplication/greptile]]. That same team also operates an [[DefinedTerm/ai-final-gatekeeper]] check after human approval, though the post does not say which of its tools performs it. The author describes the scenarios for it as effectively unlimited and calls it a strong lever for productivity and for parallel development, with the team's members reported as enthusiastic users.

The claim that post makes most directly about the customization is comparative: building a flow shaped to the team's needs produced markedly better review quality than simply handing over the guidelines and asking for a review. That is the team's own assessment from use, offered without measurement.

The DMM account is the counter-case, and it is about adoption rather than capability. That team built its auto-approval mechanism in July 2025 and reports that, despite workable accuracy and stable operation, it did not become established within the team. The reason that post gives is not a property of the action but of what was being automated: it argues that code review is a dialogue for sharing intent as well as a quality check, and that a mechanism which approves a pull request without that exchange removes the part the team valued. It proposes splitting review into a code-quality layer suited to AI and an intent-and-judgement layer left to people, which would place this kind of scripted scoring in the first layer only. That is one team's experience report, and the two accounts here disagree about outcome rather than about what the action does: both describe writing a custom flow and both report it working, while one team kept theirs and the other did not.

Both accounts come from engineering-blog posts by teams using the action rather than from documentation of it, so together they establish how two teams configured it and what they made of the result, and little else about the project.
