---
title: "These Aren't the Reviews You're Looking For: How Humans Review AI-Generated Pull Requests"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, agents, empirical-study, pull-requests]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.02273'
    hash: sha256:730f6134755c88620fbdf3f7484bce3b65c3370345ef9ce8ff858915d757ac84
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An EASE 2026 short paper comparing how humans review AI-generated pull requests against human-authored ones in the same GitHub repositories, using the AIDev dataset."
  author: ["Kacper Duma", "Patryk Wróblewski", "Jagoda Bobińska", "Julia Winiarska", "Piotr Przymus"]
  datePublished: "2026"
  keywords: ["code review", "AI-generated pull requests", "agentic workflows", "human oversight"]
---

A short paper by five authors at Nicolaus Copernicus University, Toruń, presented at the 30th International Conference on Evaluation and Assessment in Software Engineering (EASE 2026) in Glasgow. It studies how humans actually respond to pull requests authored by coding agents, a question the authors say almost nothing was known about despite agent-authored contributions becoming common.

The study draws agent-authored and human-authored pull requests from the [[Dataset/aidev]] dataset, restricted to repositories with at least 100 stars, and supplements AIDev's review records with additional data retrieved through the GitHub REST API. Two repository sets are compared: all repositories containing at least one agent-authored PR, and the intersection of those with repositories containing human-authored PRs, so that the two author types can be compared within the same projects. A rule-based regular-expression classifier assigns each human-authored review comment to one of three categories — agent steering, automation/CI interaction, or direct human review — reaching 96.5% accuracy (772 of 800) against a manually re-labelled stratified sample.

The authors' central claim is structural rather than quantitative: human participation does not disappear when the author is an agent, but the form it takes changes, shifting away from standalone evaluation and toward steering an agent through the PR's comment thread.

## Key Points

- Of 33,596 agent-authored pull requests in popular repositories, 61.38% (20,621) received no recorded review activity at all, and 38.62% (12,975) received at least one review.
- Among reviewed agent-authored PRs, 58.77% (7,625) were reviewed exclusively by agents and only 10.14% (1,316) received human-only review, with 4,034 involving mixed human–agent participation.
- Viewed as observable human involvement, 84.0% (28,246 of 33,596) of agent-authored PRs either received no recorded review or were reviewed only by agents.
- At the comment level, 71.58% of the 39,122 review comments on agent-authored PRs were written by agents and 28.42% by humans; within the human comments, 64.53% were direct human review, 28.37% were agent-steering, and 7.10% were automation-related.
- Within the same repositories, the overall rate of observable human participation was nearly identical for agent-authored and human-authored PRs (30.1% versus 30.8%) — the paper's argument is that the difference lies in composition, not in presence.
- Human-authored PRs were substantially more likely to receive human-only review (25.21%) than agent-authored ones (8.08%), while mixed human–agent review was more common on agent-authored PRs (34.29% versus 21.86%); this difference carried a moderate effect size (Cramér's V = 0.25).
- The strongest divergence the paper reports is in the mix of human comment categories (Cramér's V = 0.34): agent-steering accounted for 25.92% of human comments on agent-authored PRs against 1.63% on human-authored ones, while direct human review fell from 93.56% to 65.53%.
- The authors argue that using PR comments to steer agents blurs the boundary between evaluation and interaction, so conventional review metrics should not be read directly as measures of human oversight.

## Notes

The authors are explicit that the absence of recorded review activity does not establish the absence of human oversight — maintainers may inspect a pull request without leaving a traceable comment — and they present their results as describing observable interaction patterns rather than documented reasoning. All PRs without comments are nonetheless classified as not reviewed, because the paper says there is no empirical basis for distinguishing a silent approval from no review at all.

Several limitations are stated by the authors. Review comments are classified deterministically, so short or ambiguous comments may be misclassified; misclassifications observed in validation fell mainly between the agent-steering and human-review categories. Differences in review activity may also be influenced by factors the study does not control for, such as pull request size, complexity, or repository-specific workflows. The analysis is limited to GitHub repositories in the AIDev dataset, and the comparison further restricts to repositories containing both agent- and human-authored pull requests, so the authors caution that the results may not generalise to other settings. The paper reports descriptive results only and does not assess code quality or review effectiveness.

A replication package is published at <https://github.com/ncusi/reviewing-ai-generated-prs-ease2026-short> .
