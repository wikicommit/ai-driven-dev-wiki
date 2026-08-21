---
title: "From Industry Claims to Empirical Reality: An Empirical Study of Code Review Agents in Pull Requests"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, empirical-study, pull-requests, agent-evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.03196'
    hash: sha256:d341905668ac335fd8b65234aab88d9e6141be72f0b9ffda8fc58381845ae5e6
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An MSR '26 empirical study of code review agents on GitHub pull requests, comparing merge outcomes for CRA-only versus human-only reviews and measuring the signal-to-noise ratio of automated review comments."
  author: ["Kowshik Chowdhury", "Dipayan Banik", "K M Ferdous", "Shazibul Islam Shamim"]
  datePublished: "2026"
  abstract: "Analyses 3,109 pull requests from the AIDev dataset to compare human-only against CRA-only review, finding a 45.20% merge rate for CRA-only PRs against 68.37% for human-only, and that 60.2% of closed CRA-only PRs fall into the 0–30% signal-to-noise range."
  keywords: ["AI code review", "automated code review", "pull requests", "code review agents", "signal-to-noise ratio", "merge rates", "GitHub"]
  citation: ""
---

"From Industry Claims to Empirical Reality" is an empirical study of [[DefinedTerm/code-review-agent]] effectiveness on GitHub pull requests, presented at the 23rd International Conference on Mining Software Repositories (MSR '26) in Rio de Janeiro. Its authors are affiliated with Kennesaw State University and Quanta Technology. The paper sets itself explicitly against vendor claims: it opens from the industry position that code review agents can handle 80% of pull requests in open-source repositories with no human involvement, and asks whether the empirical record supports that.

The method is observational rather than experimental. From the [[Dataset/aidev]] dataset's 19,450 pull-request review comments the authors derive 3,109 unique PRs with at least one review comment, classify each PR's reviewer composition into five categories (CRA-only, human-only, and three mixed variants), and compare merge, closure and stall outcomes. A second stage examines the 98 closed CRA-only PRs and scores each comment for actionable content using a two-tier keyword framework, computing a signal-to-noise ratio per PR.

Its conclusion is that code review agents should augment rather than replace human reviewers, and that human involvement remains critical for effective and actionable code review.

## Key Contributions

- **A merge-rate gap.** CRA-only reviewed PRs merged 127 of 281 times, a 45.20% merge rate, against 804 of 1,176 (68.37%) for human-only reviewed PRs — a 23.17 percentage-point difference. Abandonment moves the same way: 34.88% closure for CRA-only against 21.60% for human-only. A chi-squared test of independence between reviewer type and outcome gives χ² = 83.0319 with 8 degrees of freedom and p < 0.001.
- **Mixed review sits in between.** Human-dominated reviews merged at 67.99%, CRA-dominated at 63.25%, and balanced mixed at 61.09% — the paper's evidence that human involvement improves outcomes even when agents are also present.
- **CRAs never make the decision.** PRs reviewed solely by code review agents appear exclusively in the Commented review state; the authors report that single CRA reviewers cannot independently approve, dismiss, or request changes.
- **Most automated review comments carry little signal.** Of the 98 closed CRA-only PRs, 59 (60.2%) fall into the 0–30% signal range, 14 (14.3%) into 31–59%, 7 (7.1%) into 60–79%, and 18 (18.4%) into 80–100%.
- **Volume is not quality.** PRs with signal ratios of 0.80 or above cluster at one to three comments with ratios near 1.0, while PRs below 0.30 spread across one to eight comments with ratios near 0.0 — the paper's basis for stating that the proportion of actionable feedback, not comment count, is what matters.
- **The weakness is near-universal across agents.** Among the 13 unique CRAs found in the closed set, 12 (92.31%) show average signal ratios below 60%.
- **Recommended use is narrow.** The discussion argues for configuring CRAs for specific checks such as security vulnerabilities or style violations rather than general-purpose review, enforcing human approval before merge, and establishing workflows where a CRA comment triggers human review rather than a direct developer response.

## Notes

The authors state their own limits plainly. The keyword-based signal classification may miss actionable feedback that uses no keyword, or mislabel comments that contain one irrelevantly; two researchers classified comments independently, reaching a Cohen's Kappa of 0.75. They also note that while the chi-squared test shows a statistically significant association between reviewer type and outcome, correlation does not imply causation — the study cannot show that low-signal review *caused* the abandonments it counts. External validity is bounded to open-source GitHub repositories containing AI-generated code, and the paper says the findings may not generalise to proprietary repositories, other platforms, or projects without CRAs.

Several per-agent figures rest on very small samples and should be read accordingly: one agent reaches a 100.00% average signal ratio on a single reviewed PR, while the highest ratio among agents with more substantial counts is 52.29% across 7 PRs.
