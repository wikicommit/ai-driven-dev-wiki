---
title: "AI Writes Faster Than Humans Can Review: A Longitudinal Study of an Enterprise \"2×\" Mandate"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, code-review, software-process]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.01904'
    hash: sha256:ac81932d187a0f04216eab577aedce77c1d9ea1291614c3259c025f94361d3b2
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A 2026 longitudinal case study of a documented enterprise AI mandate, tracking 802 developers and 196,212 pull requests over 28 months. It finds per-capita throughput roughly doubled — driven by adoption and accumulated use rather than by the mandate itself — and that the added volume was absorbed by shifting code review onto automation."
  author: ["Hao He", "Shyam Agarwal", "Yegor Denisov-Blanch", "Pavel Azaletskiy", "Sanmi Koyejo", "Bogdan Vasilescu"]
  datePublished: "2026"
  keywords: ["AI Mandate", "Developer Productivity", "Code Review", "Difference-in-Differences"]
---

"AI Writes Faster Than Humans Can Review" is a quantitative case study by researchers at Carnegie Mellon University and Stanford University of a documented enterprise "2×" [[DefinedTerm/ai-mandate]] — a mid-sized B2B software company whose CTO announced, in a subsequently published June 2025 memo, a goal of doubling engineering productivity through AI adoption over twelve months, with merged pull requests per engineer per month as the progress metric. The company granted research access to its internal AI-tool telemetry and pull-request history, which the authors mine into a developer-month panel of 802 developers and 196,212 non-bot pull requests across 364 active repositories, spanning January 2024 to April 2026. The authors describe the site deliberately as near-ideal rather than representative: young, AI-forward and permissive, provisioning commercial AI coding tools without per-seat caps or token budgets, so the effects are better read as an upper envelope than an industry average.

The study's method is a staggered difference-in-differences design that makes each developer their own control, lining developers up on their own adoption month rather than on the mandate date — the authors argue the mandate is a single shared date whose direct effect cannot be separated from any other organization-wide trend, whereas adoption is staggered and leaves a within-developer signature. Its three findings are that a near-doubling is attainable but accrues gradually with accumulated use rather than arriving on announcement; that the gain is broadly shared across seniority yet concentrated in newer code and not separable across model generations; and that the organization absorbed the added volume by relocating code review onto automation. The authors characterize an enterprise AI mandate as "a process-redesign problem, not a tooling deployment", because the gain relocates work downstream rather than removing it.

## Key Points

- Reports that mean pull requests per active developer rose from 21.2 in the pre-mandate baseline (January–April 2025) to 44.3 in April 2026, a 2.09× increase, which the authors state is among the largest gains reported from a field deployment of AI coding tools; company-wide pull-request volume grew 3.1× over the same window.
- Decomposes the within-developer gain into a one-time adoption jump and a gain that grows with cumulative use, and reports the two together as +0.54 log points (1.72×) under the baseline specification and +0.38 (1.46×) once full calendar-month fixed effects absorb every organization-wide monthly shock — the more conservative figure being carried as the headline. Traced month by month, the adoption effect rises from 1.51× at three months to 1.55× at six and 1.99× at nine.
- Finds the accumulated-use channel, not the one-time adoption jump, supplies the larger share of the gain, while the mandate leaves only a small residual — supporting the paper's reading of the mandate as catalytic rather than directly productive.
- Reports the adoption effect as statistically indistinguishable across the individual-contributor-to-principal ladder (+27% to +42%), with management the exception at roughly +86%; the authors read this as a re-entry effect amplified by a low base, arguing that as the cost of producing code falls, the line between directing and performing engineering work narrows.
- Finds the gain concentrated in newer code: +44% in post-2022 repositories against a non-significant +12% in legacy pre-2022 ones, a difference itself statistically significant.
- Argues the productivity gain cannot be attributed to particular frontier-model releases: the incremental release-ladder coefficients flip sign, and a placebo indicator inserted at August 2025 — a month with no model launch — moves as much as the genuine release dates, which the authors read as the design capturing calendar drift rather than capability.
- Reports that review supply did not keep up: pull-request volume grew 3.1× while the pool of developers acting as reviewers grew only 1.5×, so per-reviewer load roughly doubled.
- Finds the gap absorbed mainly by automation rather than by reviewing faster — the share of pull requests receiving at least one human review fell from 89% to 68% while the share receiving an automated AI review climbed from about 19% to about 84%, overtaking human review shortly after the mandate.
- Reports that the human review which remained thinned toward bare approval: substantive review (reviews carrying a human-written comment) fell from about 39% to about 21% of pull requests while silent approvals held roughly flat at about 50%, and at the median a reviewer's commented reviews stayed flat (~3/month) while their silent approvals roughly doubled.
- Finds merge rates essentially flat and revert rates, if anything, declining, with AI-labelled pull requests reverted slightly less than comparable human ones — but explicitly frames these as coarse, short-horizon proxies that miss defects, incidents and maintainability, reading them as evidence against an acute quality collapse rather than a clean bill of health.
- Locates the per-pull-request cost of AI authorship in latency rather than rework: AI-labelled pull requests take about 20% longer from first human review to merge and 22% longer in total cycle time, while review rounds and human-review coverage stay flat — which the authors interpret as more reviewer engagement, not more fixing.
- Recommends against governing by the merged-pull-request count alone, arguing that an authoring speedup shifts the binding constraint to stages paced by human judgment, and that velocity-centric frameworks such as DORA and SPACE register the speedup but miss where the displaced work went.

## Notes

The authors are explicit about the limits of the causal reading. The rollout was not randomized — developers chose when to adopt and how heavily to use AI — so the adoption jump rests on a parallel-trends assumption supported by flat pre-adoption trends, and the accumulated-use slope is treated as an association rather than a clean causal estimate, since cumulative AI use co-moves with workload, motivation and task mix and is partly a mechanical byproduct of shipping more code. The heavy/average/light dose-response gradient conditions on realized post-adoption usage, a post-treatment variable, so it is presented as descriptive. The authors frame the headline as a throughput doubling that within-developer and dose-response evidence strongly implicate adoption and accumulated use in, while treating the exact causal magnitude as bounded rather than point-identified.

The throughput estimate's sensitivity to estimator choice is reported as itself informative: the adoption coefficient is +0.354 under the baseline two-way fixed-effects design, +0.201 with full calendar-month fixed effects, +0.369 dropping never-treated developers, +0.132 under Borusyak imputation, and shrinks to a non-significant +0.162 under Callaway–Sant'Anna. The authors argue the attenuation is localized rather than a failure of the result, since only estimators that forbid already-adopted developers from serving as controls pull it toward zero — a restriction that understates an effect which grows with use.

External validity is bounded twice by the authors' own account: the estimates come from one young, AI-forward firm, and that firm made the merged-pull-request count its official progress metric, so a broadcast target invites inflation the design cannot fully separate from genuine acceleration. Identification of AI-authored pull requests relies on the company's own `created-by-ai` label, applied by a mechanism outside the researchers' control, so per-pull-request AI-versus-human comparisons are treated as correlational and causal claims reserved for the developer-panel design. A caveat specific to the window's tail is that the company began routing pull requests through AI-driven review and auto-approval late in the period, collapsing human-review latency for a growing share of them and biasing the measured latency premium toward zero.
