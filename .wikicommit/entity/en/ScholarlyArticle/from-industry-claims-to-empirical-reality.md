---
title: "From Industry Claims to Empirical Reality: An Empirical Study of Code Review Agents in Pull Requests"
type: "schema:ScholarlyArticle"
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
  description: "An empirical study of 3,109 GitHub pull requests drawn from the AIDev dataset, comparing merge outcomes between pull requests reviewed only by humans and those reviewed only by code review agents. It reports a 23.17 percentage point merge-rate gap in favour of human-only review, and links the gap to low signal-to-noise ratios in agent-generated review comments."
  author: ["Kowshik Chowdhury", "Dipayan Banik", "K M Ferdous", "Shazibul Islam Shamim"]
  datePublished: "2026-04"
  keywords: ["AI code review", "automated code review", "pull requests", "code review agents", "signal-to-noise ratio", "merge rates", "GitHub"]
---

This paper sets a claim made in industry reporting against repository data. The claim it takes
as its foil is that [[DefinedTerm/code-review-agent]] deployments can handle around 80% of pull
requests with no human comment at all — a figure the authors attribute to reports from Qodo and
Greptile. Against this they set the empirical picture they read from prior work: that agent
comments are acted on far less often than human ones. Their stated goal is to establish when and
how code review agents (CRAs) actually influence whether a pull request merges, by looking at two
things — who reviewed it, and how much of what the reviewer said was worth acting on.

The study works from [[Dataset/aidev]], taking the 3,177 pull requests in it that carry at least
one review comment and then excluding bot accounts that perform CI/CD and workflow automation
rather than code review, which leaves a working set of 3,109. Each PR is labelled by reviewer
composition — human-only, CRA-only, or one of three mixed categories — and by outcome: merged,
closed without merging (read as abandonment), or still open. Because pull requests reviewed solely by CRAs turn out to
occur only in the Commented review condition, the authors restrict the human-versus-agent
comparison to the 2,456 PRs in that condition. For the second research question they take the 98
closed CRA-only PRs and score each one's comments using a
[[DefinedTerm/signal-to-noise-ratio]] measure, classifying comments against two keyword tiers.

The headline result is a 45.20% merge rate for CRA-only reviewed PRs against 68.37% for
human-only ones, with abandonment running at 34.88% versus 21.60%. The signal analysis offers the
authors' explanation for the gap: most of the abandoned pull requests carried predominantly
noisy comments.
Their recommendation to practitioners is correspondingly narrow — that CRAs should augment human
reviewers rather than replace them, and should be configured for specific checks such as security
or style rather than general-purpose review.

The paper appeared at the 23rd International Conference on Mining Software Repositories
(MSR '26), held in Rio de Janeiro on 13–14 April 2026, and carries the DOI
<https://doi.org/10.1145/3793302.3793614> . It is distributed under a Creative Commons
Attribution 4.0 International License.

## Key Points

- Pull requests reviewed only by CRAs merged at 45.20% (127 of 281), against 68.37% (804 of
  1,176) for pull requests reviewed only by humans — a 23.17 percentage point difference. Both
  figures are drawn from the 2,456 PRs in the Commented review condition alone.
- CRA-only reviewed PRs were closed without merging at 34.88% (98 of 281), against 21.60% (254 of
  1,176) for human-only ones. The authors read closure-without-merge as abandonment.
- A chi-squared test of independence between reviewer type and outcome returned χ² = 83.0319 on 8
  degrees of freedom with p < 0.001. The authors state in their threats to validity that this
  establishes association, not causation.
- Mixed reviewer categories landed between the two extremes: 67.99% merge for human-dominated
  reviews, 63.25% for CRA-dominated, and 61.09% where the counts were equal. The authors take
  this as evidence that human involvement improves outcomes even where agents are also present.
- Among the 98 closed CRA-only PRs, 59 (60.2%) scored a signal ratio of 0–30%, 14 (14.3%) scored
  31–59%, 7 (7.1%) scored 60–79%, and 18 (18.4%) scored 80–100%. This distribution describes
  abandoned PRs only; the paper does not report the same breakdown for merged ones.
- Of the 13 distinct CRAs appearing in that closed set, 12 (92.31%) had average signal ratios
  below 60%. The highest per-agent averages rest on very few PRs — one agent scored 100.00% on a
  single PR, and the best-performing agent with a meaningful count reached 52.29% across 7.
- PR count and feedback quality were unrelated in the sample: the two agents with the largest
  shares of the closed set scored 27.62% (36 PRs) and 19.79% (24 PRs).
- Comment volume did not by itself predict quality. The authors report that the highest-scoring
  PRs clustered at one to three comments, while the lowest-scoring ones spread across one to
  eight, and conclude that the proportion of actionable feedback is what matters.
- Pull requests reviewed solely by CRAs appeared exclusively in the Commented review condition.
  The authors read this as showing that a lone CRA reviewer cannot approve, dismiss, or request
  changes on its own.

## Notes

The paper positions itself against two bodies of work. On the industry side it cites vendor
reports and blog posts claiming high autonomous-review coverage; these are the claims the title's
"industry claims" refers to, and the paper treats their figures as claims to be tested rather
than as established results. On the research side it cites prior studies of what agent-authored
pull requests change, of maintainer perceptions of review bots, and of whether language models
understand review content at all — arguing that none of them connect reviewer composition and
comment quality to merge and abandonment outcomes, which is the gap it claims to fill.

The authors state three limitations of their own. Their keyword-based signal classification may
miss actionable feedback that uses no matching keyword, and may label keyword-containing but
irrelevant comments as signal; they report manual validation and two independent raters as
mitigation. They note that manual classification can introduce bias. And they restrict their
external validity claim to open-source GitHub repositories containing AI-generated code, saying
the findings may not carry over to proprietary repositories, other platforms, or projects that do
not use CRAs at all.

The analysis code and derived data are stated to be publicly available through a Figshare
deposit.
