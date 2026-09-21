---
title: "Review Bottleneck"
type: "schema:DefinedTerm"
lang: en
tags: [agents, code-review, software-process]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.01904'
    hash: sha256:ac81932d187a0f04216eab577aedce77c1d9ea1291614c3259c025f94361d3b2
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60882/'
    hash: sha256:7997cccac08ed6a2731d85a3012e81cea6de4b141192497c171f97de0740feb1
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The downstream congestion that follows when AI accelerates code authoring while human review capacity stays fixed, so surplus work accumulates at the review stage rather than being removed."
---

The review bottleneck is the congestion that arises when AI accelerates the authoring of code while human review capacity stays fixed, so surplus work accumulates downstream rather than disappearing. [[ScholarlyArticle/ai-writes-faster-than-humans-can-review]] describes it as the outcome a capacity-constrained rollout predicts, and reports it directly: over the study window pull-request volume grew 3.1× while the pool of developers acting as reviewers grew only 1.5×, so demand outran review supply and per-reviewer load roughly doubled. The paper's broader framing is that an AI mandate relocates work downstream rather than removing it, and that the binding constraint moves to whichever stages are paced by human judgment.

## Usage

What the paper documents is not a queue that simply grew, but an organization that responded by changing what review *is*. The share of pull requests receiving at least one human review fell 21 percentage points, from 89% to 68%, while the share receiving an automated AI review climbed from about 19% to about 84% — overtaking human review shortly after the mandate, which the authors describe as a progressive shift toward relying on automated review in place of, not merely alongside, human review.

The human review that remained also thinned. Its substantive part — reviews carrying a human-written comment — fell from about 39% to about 21% of pull requests while silent approvals held roughly flat at about 50%; at the median, a reviewer's commented reviews stayed flat at around three a month while their silent approvals roughly doubled. The authors' reading is that the added load fell on bare approval rather than on substantive review.

At the level of an individual change, the cost showed up as latency rather than rework. Controlling for author, month and change size, AI-labelled pull requests took about 20% longer from first human review to merge and about 22% longer in total cycle time, while review rounds and human-review coverage stayed flat and the per-change comment premium was small. The authors argue this rules out the two competing explanations — more buggy changes would pass through more review rounds, and changes merged with less scrutiny would draw less review — leaving more reviewer engagement without more fixing.

The organization-level counterpart is that the aggregate queue never actually decongested. The 90th-percentile end-to-end cycle time climbed through 2025, peaking near 66 hours, then receded in 2026; but decomposed by review depth, the same figure for pull requests that received a substantive human review climbed to its own peak near 114 hours and remained around 73 hours in 2026, above its roughly 63-hour pre-ramp level. What fell was the *share* of changes routed through substantive review, from a pre-mandate peak of about 48% to about 21%. The authors conclude that the company kept pace by routing work around human review rather than by reviewing faster.

Coarse quality proxies did not move: merge rates stayed essentially flat and revert rates, if anything, declined. The paper is careful about how far that goes, noting that merge and revert are short-horizon measures that miss defects, incidents and maintainability, and reading them as evidence against an acute quality collapse rather than a clean bill of health. It names what its own data cannot see — what a machine reviewer misses, and what developers stop learning as review moves off them — as open questions.

A practitioner account of the same constraint, from a different vantage, is
[[BlogPosting/redesigning-code-review-for-the-ai-era]]. There a team that adopted coding agents
saw its commit count roughly double, and states the asymmetry directly: a matching doubling of the
hours engineers spend reviewing is hard to arrange, so without a change to the flow, falling code
quality is what the post says follows. It adds a reason of its own for why the load is worse than the
volume suggests — that faults in AI-generated code are harder for a human to spot, which raises
the cost of each review rather than only their number — and identifies reviewer load as the
bottleneck on the productivity the agents were adopted for.

What that account contributes beyond the study is the response rather than the measurement. Its
team's answer is to attack both terms of the ratio: raise the quality of pull requests before they
reach a human, through written guidelines and a [[DefinedTerm/testing-skyscraper]] testing
strategy, and speed up the reviewing that remains, through AI reviewers and standardized agent
skills. It reports its backend team's test-to-code line ratio rising from 78.6% to 112.6% over six months.
That is one team's experience rather than a measured comparison, and it should be read as such
next to the study above; it is notable here mainly because it converges on the same diagnosis
from inside one organization rather than across many.

## Related Terms

[[DefinedTerm/ai-mandate]], [[DefinedTerm/code-review-agent]], [[DefinedTerm/verification-debt]], [[DefinedTerm/signal-to-noise-ratio]], [[DefinedTerm/code-review-as-runtime-monitoring]], [[DefinedTerm/ai-final-gatekeeper]]
