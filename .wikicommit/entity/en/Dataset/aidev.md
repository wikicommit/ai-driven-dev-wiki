---
title: "AIDev"
type: "schema:Dataset"
lang: en
tags: [agents, code-review, software-engineering]
sources:
  - type: url
    url: https://arxiv.org/pdf/2604.03196
    hash: sha256:d341905668ac335fd8b65234aab88d9e6141be72f0b9ffda8fc58381845ae5e6
    license: CC-BY-4.0
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "A dataset of pull request review activity from open-source GitHub repositories containing AI-generated code, published on Hugging Face and used as the empirical base for research on automated code review."
  url: "https://huggingface.co/datasets/hao-li/AIDev/viewer/pr_review_comments"
  variableMeasured: ["user", "user_type", "body", "pull_request_url", "review state", "PR state", "merged_at", "pr_id", "pull_request_review_id"]
---

AIDev is a dataset of pull request activity drawn from open-source GitHub repositories that
contain AI-generated code. It is published on Hugging Face, and its value for research is that it
captures both sides of the agentic pull request at once — the review comments left on a pull
request, together with what eventually happened to that pull request. That pairing is what allows
a study to ask whether a particular kind of reviewer is associated with code actually landing.

## Contents

The dataset is organised into several linked tables. The one carrying review comments is
`PRReviewComment`, in which each record holds the name of whoever posted the comment, a
categorical `user_type` marking that account as either `User` or `Bot`, the comment text itself,
and an API endpoint identifying the parent pull request. Note that the `Bot` value covers every
automated account without distinguishing a reviewer from a build runner, so separating
[[DefinedTerm/code-review-agent]] accounts from CI/CD ones requires manual classification.

A `PRReview` table supplies the review state, which takes one of four values: `COMMENTED` for
general feedback carrying no explicit decision, `APPROVED`, `CHANGES_REQUESTED`, or `DISMISSED`.
A `PullRequest` table supplies the pull request's own state — open or closed — and a `merged_at`
timestamp that is null where the pull request was never merged, which together make it possible
to tell a merged pull request from an abandoned one. The tables join on `pr_id`, and comment-level
data attaches through `pull_request_review_id`.

On scale, the figure reported for the `PRReviewComment` table is 19,450 records; the same figure
is also described as 19,450 pull requests carrying review activity, so it is safest read as the
size of the review-comment table rather than as a confirmed count of distinct pull requests.
Filtering that material down to pull requests with at least one review comment yields 3,177
distinct pull requests.

## Provenance

AIDev is distributed through Hugging Face under the `hao-li` namespace. Its coverage is limited
to open-source GitHub repositories containing AI-generated code, which bounds what can be
concluded from it: findings drawn from AIDev do not automatically extend to proprietary
repositories, to other hosting platforms, or to projects that make no use of automated review.

## Use

[[ScholarlyArticle/from-industry-claims-to-empirical-reality]] used AIDev to compare merge
outcomes across reviewer types. Working from the 3,177 pull requests with at least one review
comment, it excluded bot accounts performing CI/CD and workflow automation rather than code
review, arriving at a working set of 3,109 pull requests reviewed by actual code review agents.
Of those, 2,456 fell into the Commented review condition, which the study used as the basis for
its human-versus-agent comparison because pull requests reviewed solely by agents occurred
nowhere else.
