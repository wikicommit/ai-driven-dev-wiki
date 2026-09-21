---
title: "CodAGE"
type: "schema:Dataset"
lang: en
tags: [agents, mining-software-repositories]
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
  description: "Coding Agent-generated GitHub Events: a public dataset of GitHub events attributable to AI coding agents, collected from GHArchive and divided into event-type subsets covering pull requests, reviews and review comments."
  url: "https://huggingface.co/datasets/taher-ghaleb/CodAGE"
---

CodAGE — Coding Agent-generated GitHub Events — is a public dataset of GitHub events attributable to AI coding agents. It is used as the source data for [[ScholarlyArticle/ai-to-ai-code-reviews-of-github-pull-requests]], which draws its population of agent-authored and agent-reviewed pull requests from it.

## Contents

The dataset is divided into several event-type subsets. The three drawn on by the study above are CodAGE-PRs, which carries pull-request authorship signatures, and CodAGE-Reviews and CodAGE-ReviewComments, which carry reviewer-side activity.

Its scale is visible in the counts that study reports from the snapshot it used: a broad first attribution pass over CodAGE-PRs yielded 4,563,819 candidate pull requests carrying a provisional agent label, while the two review-side streams held 4,141,598 review events and 8,560,919 review comments.

That first pass includes branch-name evidence. The study above then applied its own two-tier signature framework as a stricter second pass over the same pool — requiring a body signature or a vendor-controlled login, and discarding branch-name-only matches — which is what reduced those 4.5 million candidate PRs to 2,830,284 attributed agent-authored ones. The study notes that both passes are its own, so the comparison between them is an internal consistency check rather than external validation.

## Provenance

CodAGE is collected from GHArchive, so its coverage is public GitHub events and excludes private repositories, GitHub Enterprise deployments and other version-control platforms. It is published on Hugging Face at <https://huggingface.co/datasets/taher-ghaleb/CodAGE> under CC BY 4.0.

The snapshot used by the study above covers 1 January 2024 to 15 April 2026. That study notes two timing points about working from it: despite the window covering the relevant period, many autonomous AI coding agents emerged only in early 2025; and GHArchive attributes lag event data by roughly a quarter, which makes the most recent quarter's counts lower bounds.

## Use

[[ScholarlyArticle/ai-to-ai-code-reviews-of-github-pull-requests]] used it to build a dataset of [[DefinedTerm/closed-loop-ai-review]] — pull requests authored by one AI coding agent and reviewed by another — reporting 248,641 agent-authored PRs that received at least one AI-attributed review, and measuring how reviewer output varied with the authoring agent and with same- versus cross-product pairing.
