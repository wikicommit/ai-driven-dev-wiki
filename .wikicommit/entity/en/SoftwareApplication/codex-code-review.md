---
title: "Codex Code Review"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, coding-agents, agent-config]
sources:
  - type: url
    url: 'https://developers.openai.com/blog/custom-code-review-rules-for-codex'
    hash: sha256:545da2cc607e493ec8565ebfedabe86da5990d39d08e426344d54fa68908973a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "OpenAI's pull-request review capability for Codex, which reviews changes in a GitHub repository and, since July 2026, can apply custom repository rules written in AGENTS.md and cite the relevant rule in its findings."
  applicationCategory: "AI code review"
  featureList: "Pull-request review on GitHub repositories; on-demand review via @codex review; custom repository rules read from root and nested AGENTS.md files; findings that cite the applicable rule, location and priority"
  author: "[[Organization/openai]]"
---

Codex Code Review is the code-review capability of [[SoftwareApplication/openai-codex]]. OpenAI documents turning it on for a GitHub repository, and a review can also be requested directly with `@codex review`. [[BlogPosting/custom-code-review-rules-for-codex]] announced that it can use custom repository rules written in [[DefinedTerm/agents-md]] to catch issues specific to a codebase and to point authors to the guidance behind each finding.

OpenAI presents the feature as a response to review becoming the bottleneck once coding agents produce more code: repository rules let context that normally lives with a few experienced reviewers — an API contract to preserve, data to keep out of logs — sit next to the code it applies to, where contributors or coding agents new to that part of a repository can benefit from it.

## Capabilities

Rules live in `AGENTS.md`, the same file that guides Codex's coding tasks. Repository-wide rules go at the root and service-specific rules in the relevant directory; during review, Codex applies the guidance that covers the changed files and cites it in the finding. OpenAI's example is a breaking-change rule in the Codex repository that protects an app-server notification consumed by Codex Cloud: a rename that still compiles would draw a finding explaining that consumers listen for the existing name and that the author should keep it or add a backward-compatible event.

OpenAI reports that in its primary eval suite, rule-guided variants recovered 98% of the required custom findings against 58.3% for a baseline control, and that it also tested whether clean changes avoided unnecessary findings, whether ordinary bugs outside the rules were still caught, and whether findings named the relevant guidance, location and priority.

## Adoption & Ecosystem

OpenAI's guidance is to keep deterministic and mechanical checks in tests, linters and CI and to reserve repository rules for judgment calls, starting with two or three rules for consequential, non-obvious invariants and refining them from what a representative pull request produces. It describes the tool as an additional reviewer rather than an enforcement mechanism: tests, branch protections and required approvals continue to provide hard enforcement. It sits among other AI review tools covered in this wiki under [[DefinedTerm/agentic-code-review]].
