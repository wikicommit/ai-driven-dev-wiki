---
title: "Claude Code Action"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, agents, ci, coding-tools]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60882/'
    hash: sha256:7997cccac08ed6a2731d85a3012e81cea6de4b141192497c171f97de0740feb1
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A GitHub Action that runs a Claude Code agent against a pull request, so review, CI-failure diagnosis and follow-up work can happen on the PR page itself. Its review flow is scriptable, which one team used to build a multi-phase review of its own."
  applicationCategory: "AI code review"
  featureList: "Runs a Claude Code agent on GitHub pull requests; scriptable multi-phase review flows with subagents; CI-failure diagnosis and fixing from the PR; responding to review comments and opening follow-up PRs"
  author: "[[Organization/anthropic]]"
---

Claude Code Action is a GitHub Action that puts a [[SoftwareApplication/claude-code]] agent on a pull request. [[BlogPosting/redesigning-code-review-for-the-ai-era]] describes a team adopting it for a specific reason: its members already spent their day on the GitHub PR screen checking comments and CI status, and the post's thought was that being able to carry code review through on that same screen would be considerably more efficient.

The property that post treats as decisive is how far the review flow can be shaped: it rates the freedom to customize as considerable, and in its comparison of three tools rates this one's customizability "unlimited" against "high" for [[SoftwareApplication/greptile]] — which it credits with auto-learned custom rules — and "medium" for GitHub Copilot. Rather than tuning a fixed review, the team wrote its own flow and had the action run it.

## Capabilities

- Runs a Claude Code agent against a pull request, where it can be used for code review, for diagnosing and fixing CI failures, and for acting on review comments including opening a new pull request from them.
- Review flows are scriptable as multiple phases with subagents assigned to separate concerns. The flow the post's team built, modelled on Claude's own published code-review example, runs four: a preparation phase gathering PR metadata, the issue being solved, the author, the development area and the guidelines applying to it; a review phase with one subagent per review perspective working against those guidelines; a severity-evaluation phase whose subagent judges whether each AI comment is valid, not fabricated, and how serious it is; and a posting phase that inline-comments only the high-severity findings, sends a summary, and suppresses anything another agent has already said.
- Rated in the post as the strongest of the three tools compared on domain understanding, and high on review quality; deep codebase understanding is listed among its characteristic features rather than scored against the others.
- Its reported drawbacks: setup is rated fiddly, which the post attributes to needing care around permissions, and it is the slowest of the three to review. The post also notes that deciding between an API key and a personal token is difficult on the Enterprise edition.

## Adoption & Ecosystem

The post's team runs it as one of three AI reviewers alongside GitHub Copilot and [[SoftwareApplication/greptile]]. That same team also operates an [[DefinedTerm/ai-final-gatekeeper]] check after human approval, though the post does not say which of its tools performs it. The author describes the scenarios for it as effectively unlimited and calls it a strong lever for productivity and for parallel development, with the team's members reported as enthusiastic users.

The claim the post makes most directly about the customization is comparative: building a flow shaped to the team's needs produced markedly better review quality than simply handing over the guidelines and asking for a review. That is the team's own assessment from use, offered without measurement.

Everything recorded here comes from a single engineering-blog post that uses the action rather than documenting it, so it establishes how one team configured it and what they thought of the result, and little else about the project.
