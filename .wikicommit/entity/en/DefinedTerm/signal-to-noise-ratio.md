---
title: "Signal-to-Noise Ratio (Code Review)"
type: "schema:DefinedTerm"
lang: en
tags: [agents, code-review]
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
  description: "A measure of review feedback quality: the share of a pull request's review comments that raise an actionable problem, expressed as a ratio from 0.0 to 1.0. Used to judge automated review output where comment volume alone says nothing about usefulness."
---

Applied to code review, the signal-to-noise ratio is the proportion of the review comments on a
pull request that raise something worth acting on. It is computed as the number of comments
carrying critical or important signal divided by the total number of comments, giving a value
between 0.0, where nothing said was actionable, and 1.0, where everything was. Its purpose is to
separate how much a reviewer said from how much of it mattered — a distinction that becomes
important once the reviewer is automated and the cost of producing another comment falls to
nearly nothing.

## Usage

The measure requires a rule for deciding which comments count as signal.
[[ScholarlyArticle/from-industry-claims-to-empirical-reality]] operationalises it with two
keyword tiers. Tier 1, critical signal, covers runtime errors, crashes, compilation failures,
API-breaking changes, and security vulnerabilities. Tier 2, important signal, covers
architectural problems, performance issues, and maintainability concerns. Comments matching
either tier count toward the numerator; everything else is noise.

That study also groups the resulting ratios into four bands, chosen so that each band says
whether signal or noise dominates: 0–30% is predominantly noisy, with under a third of comments
actionable; 31–59% is more noise than signal; 60–79% is more signal than noise; and 80–100% is
predominantly actionable. It treats 0.60 and 0.80 as the thresholds for good and great feedback
respectively.

Applied to 98 abandoned pull requests that had been reviewed only by a
[[DefinedTerm/code-review-agent]], the measure put 60.2% of them in the lowest band, and found 12
of the 13 agents involved averaging below 60%. The same analysis found that comment volume and
signal ratio were largely independent — the highest-scoring pull requests carried only one to
three comments each, while the lowest-scoring ones spread across one to eight.

## When It Applies

The measure applies where a body of review comments exists on a unit of work and each comment can
be judged individually as raising a problem or not. It is comparative by nature: a single ratio
in isolation says little, and its use in practice is to set one reviewer, or one class of
reviewer, against another.

It assumes that actionable feedback is recognisable from the text of a comment, and that comments
are the right unit to count — that two comments raising a problem are twice as much signal as
one. It also assumes the classification rule matches what the reviewers of that codebase would
actually consider worth acting on, which the keyword tiers above fix in advance rather than
derive from the project.

The classification rule is where it fails. The authors who applied it state in their own threats
to validity that keyword matching can miss actionable feedback phrased without any of the
keywords, and can count keyword-containing but irrelevant comments as signal. They report
mitigating this with manual validation by two independent raters who discussed disagreements and
refined the keyword lists, reaching a Cohen's Kappa of 0.75 for inter-rater agreement — which
records that the manual step is itself a judgment call rather than a check that removes one. A
further misreading the measure invites is treating a high ratio drawn from very few comments as
comparable to one drawn from many: in that study the only agent scoring 100% had reviewed a
single pull request.

The measure is not an established standard. The study above adopts the framework from a blog post
it cites, and supplies the two keyword tiers and the classification procedure itself, using open
coding as the qualitative technique. Its published track record is that one application.

## Related Terms

- [[DefinedTerm/code-review-agent]] — the class of reviewer the measure has mainly been used to
  assess
