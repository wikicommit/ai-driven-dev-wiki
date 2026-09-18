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
  - type: url
    url: https://arxiv.org/pdf/2602.09185
    hash: sha256:3d94ab700934f9544d412431d530fd11f6856381d3e23f9b57ac0adcd28f9989
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A dataset of 932,791 pull requests authored by AI coding agents (Agentic-PRs) across 116,211 GitHub repositories and 72,189 developers, with a curated 33,596-PR subset from repositories with over 100 stars enriched with review, commit, and issue data."
  creator: ["Hao Li", "Haoxiang Zhang", "Ahmed E. Hassan"]
  url: "https://huggingface.co/datasets/hao-li/AIDev"
  variableMeasured: ["user", "user_type", "body", "pull_request_url", "review state", "PR state", "merged_at", "pr_id", "pull_request_review_id"]
  temporalCoverage: "../2025-08-01"
---

AIDev is a dataset of 932,791 pull requests authored by AI coding agents ("Agentic-PRs") in
real-world, open-source GitHub repositories, introduced in [[ScholarlyArticle/aidev]] by
researchers at Queen's University. It spans 116,211 repositories and 72,189 developers, with a
dataset cutoff of August 1, 2025, and aggregates PRs from five agents: OpenAI Codex, Devin, GitHub
Copilot, Cursor, and Claude Code. A curated subset of 33,596 Agentic-PRs from 2,807 repositories
with more than 100 GitHub stars is additionally enriched with review comments, commit-level diffs,
issue links, and full pull-request event timelines. Its value for research is that it lets a study
ask what happened to an agent-authored pull request — how it was reviewed and whether it was
merged — at a scale prior controlled studies and small-scale deployments did not reach.

## Contents

[[ScholarlyArticle/aidev]] groups the dataset's tables into five families. Core metadata —
`all_pull_request` (932,791 records: title, body, agent, state, timestamps, repository, user),
`all_repository` (116,211: name, license, language, URL, stars, forks), and `all_user` (72,189:
login, followers, creation date) — covers the full dataset; the curated 100+-star subset repeats
the same three tables at smaller scale (`pull_request`: 33,596, `repository`: 2,807, `user`: 1,796).
Comments & Reviews adds `pr_comments` (39,122 discussion-style comments), `pr_reviews` (28,875
review verdicts — approve or request changes), and `pr_review_comments` (19,450 inline code review
comments with file-level context: path, diff hunk, timestamp) — available only for the curated
subset. Commits & Diffs adds `pr_commits` (88,576) and `pr_commit_details` (711,923 file-level
commit diffs). Issues & Events adds `related_issue` (4,923), `issue` (4,614), and `pr_timeline`
(325,500 PR events such as committed, closed, merged, labeled, reviewed). An Annotation table,
`pr_task_type` (33,596), carries an automated, GPT-based classification of each curated PR's
purpose following the Conventional Commits categories.

[[ScholarlyArticle/from-industry-claims-to-empirical-reality]], working from the review-comment
data described above, reads the review-comment table as carrying the name of whoever posted the
comment, a categorical `user_type` marking that account as either `User` or `Bot`, the comment text
itself, and an API endpoint identifying the parent pull request. Note that the `Bot` value covers
every automated account without distinguishing a reviewer from a build runner, so separating
[[DefinedTerm/code-review-agent]] accounts from CI/CD ones requires manual classification. That
study also reads the review-state field as taking one of four values — `COMMENTED` for general
feedback carrying no explicit decision, `APPROVED`, `CHANGES_REQUESTED`, or `DISMISSED` — and a
pull request's own `merged_at` timestamp as null where the pull request was never merged, which
together make it possible to tell a merged pull request from an abandoned one.

On scale, that study filters the review-comment material down to pull requests with at least one
review comment, yielding 3,177 distinct pull requests out of the curated subset's 33,596.

## Provenance

AIDev is distributed through Hugging Face under the `hao-li` namespace, and also through Zenodo,
with example Jupyter notebooks and Google Colab links published in a companion GitHub repository.
On Hugging Face it can be explored interactively through a "Data Studio" interface supporting
in-browser SQL queries. Its coverage is limited to open-source GitHub repositories containing
AI-generated code up to its August 1, 2025 cutoff, which bounds what can be concluded from it:
findings drawn from AIDev do not automatically extend to proprietary repositories, to other hosting
platforms, to agents outside the five it covers, or to activity after its cutoff date.

## Use

[[ScholarlyArticle/from-industry-claims-to-empirical-reality]] used AIDev to compare merge
outcomes across reviewer types. Working from the 3,177 pull requests with at least one review
comment, it excluded bot accounts performing CI/CD and workflow automation rather than code
review, arriving at a working set of 3,109 pull requests reviewed by actual code review agents.
Of those, 2,456 fell into the Commented review condition, which the study used as the basis for
its human-versus-agent comparison because pull requests reviewed solely by agents occurred
nowhere else.

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] cites a study of 15,451
refactoring instances across 12,256 agent-authored pull requests, drawn from AIDev, which found
that agents frequently perform localized and consistency-oriented refactorings — such as variable
renaming and type updates — while undertaking fewer high-level architectural changes than human
developers.
