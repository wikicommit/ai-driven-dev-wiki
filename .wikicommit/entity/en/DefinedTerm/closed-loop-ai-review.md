---
title: "Closed-Loop AI Review"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-code-review, agents]
sources:
  - type: url
    url: 'https://arxiv.org/html/2608.21311v1'
    hash: sha256:fbf82284375303f9675600e80d90e76d55be064a407f52c9123f292427a990b4
    license: CC-BY-4.0
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An AI coding agent contributing to a repository and one or more AI coding agents reviewing it — AI on both sides of the pull request. The term is defined in a purely observable sense: it says that AI occupied both roles, not that no human reviewed the change."
---

Closed-loop AI review names the configuration in which an AI coding agent contributes to a repository and one or more AI coding agents review that contribution — AI on both sides of the pull request. The term is introduced in [[ScholarlyArticle/ai-to-ai-code-reviews-of-github-pull-requests]], which is careful to define it observationally: because the review events it can see are restricted to AI-attributed ones, "closed loop" means that AI occupies both roles, **not** that humans were absent. A pull request counted as closed-loop may well have received human review that simply was not visible in the data.

## Usage

The configuration exists because coding agents now occupy two distinct roles in the pull-request workflow. Authoring agents — the paper names Devin, [[SoftwareApplication/openai-codex]], [[SoftwareApplication/github-copilot-coding-agent]], [[SoftwareApplication/cursor]] and [[SoftwareApplication/claude-code]] — open PRs on a user's behalf, autonomously or as assistive tools. Reviewing agents such as [[SoftwareApplication/coderabbit]], Sourcery and PR-Agent post line-level comments and review decisions. Several products appear in both roles, which is what makes the loop close within a single ecosystem as well as across ecosystems.

A distinction the term carries in practice is between same-product and cross-product loops: whether the reviewing agent is the same identifiable product as the authoring agent, or a different one. That boundary is drawn at the level of the agentic product or harness rather than the vendor or the underlying model, so two products from one company count as cross-product. Same-product review may simply be part of an integrated product workflow, which is why the study that introduced the term treats cross-product review as the more interesting case.

## When It Applies

As a measured phenomenon it was, on the evidence available, a minority of agent activity but growing steeply: 8.8% of identified agent-authored PRs received at least one AI review, 1.6% across products, with cross-product volume rising more than two orders of magnitude between 2025-Q1 and 2025-Q3.

The term's practical weight is what it implies for anyone reading GitHub data. If an increasing share of public code is evaluated partly by AI, then studies treating review history as evidence of human decision making are mixing populations, and maintainers cannot assume review signals mean what they used to. The same argument applies downstream, to tooling that summarizes or aggregates review output.

Two cautions come with it. The configuration is identified by signature attribution, so absence of an AI signature is not evidence that no AI was involved — counts are lower bounds. And observing that AI reviewed AI says nothing about whether the review was any good: the study that named the phenomenon measured comment volume, category mix and latency, and states explicitly that these describe observable reviewer behaviour rather than review correctness or software quality.

## Related Terms

[[DefinedTerm/agentic-code-review]], [[DefinedTerm/code-review-agent]], [[DefinedTerm/llm-as-a-judge]], [[DefinedTerm/review-bottleneck]]
