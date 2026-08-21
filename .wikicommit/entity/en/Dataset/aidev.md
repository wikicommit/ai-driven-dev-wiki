---
title: "AIDev"
type: "schema:Dataset"
lang: en
tags: [pull-requests, empirical-study, agentic-coding, github]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.03196'
    hash: sha256:d341905668ac335fd8b65234aab88d9e6141be72f0b9ffda8fc58381845ae5e6
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A dataset of GitHub pull requests involving autonomous coding agents, distributed on HuggingFace and structured as linked tables covering pull requests, reviews and review comments."
  creator: ""
  datePublished: ""
  measurementTechnique: ""
  sameAs: "https://huggingface.co/datasets/hao-li/AIDev/viewer/pr_review_comments"
---

AIDev is a dataset of GitHub pull requests involving autonomous coding agents, distributed on HuggingFace and used as the empirical base for studies of agentic pull-request workflows. [[ScholarlyArticle/code-review-agents-in-pull-requests]] draws its entire analysis from it, and the description of its structure here is that paper's account of the tables it used rather than a full specification of the dataset.

## Composition

The table that study centres on is `PRReviewComment`, holding 19,450 records of pull-request review comments. Each comment carries the name or identifier of the reviewer that posted it, a `user_type` field classifying that reviewer as either "User" (human) or "Bot" (an automated agent), the textual body of the comment, and a `pull_request_url` pointing at the parent pull request.

Two further tables supply the outcome data. `PRReview` provides a review `state` attribute with the values COMMENTED, APPROVED, CHANGES_REQUESTED and DISMISSED; `PullRequest` provides the PR's open/closed state and a `merged_at` timestamp that is null when the PR was never merged. The tables join on `pr_id` and `pull_request_review_id`.

Aggregating the comment records by pull request and keeping only PRs with at least one review comment yields 3,177 unique PRs in that study's hands, reduced to 3,109 after excluding bots that perform CI/CD and workflow automation rather than code review.

## Use in Evaluation

The dataset supports outcome analysis rather than capability benchmarking: because reviewer identity, reviewer type, comment text and merge status are all linked, it can be used to compare merge and abandonment rates across reviewer compositions and to score the content of review comments. The study above used it for exactly that, deriving a 45.20% merge rate for agent-only reviewed PRs against 68.37% for human-only ones.

Its stated scope limit is that it covers open-source GitHub repositories containing AI-generated code, so findings drawn from it may not generalise to proprietary repositories, other platforms, or projects that do not use review agents at all. The same study notes as a strength that the repositories it covers span diverse domains, sizes, and maturity levels.
