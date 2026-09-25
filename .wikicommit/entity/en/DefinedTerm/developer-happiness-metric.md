---
title: "Developer Happiness Metric"
type: "schema:DefinedTerm"
lang: en
tags: [code-completion, evaluation-metrics, developer-experience]
sources:
  - type: url
    url: 'https://habr.com/ru/companies/yandex/articles/841436/'
    hash: sha256:ed090e4e81e25e3fc5fbdddabb08371c8ae7509c5d4943bdcadbc1d5a5459eff
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A composite online metric that Yandex's Code Assistant team devised for inline code suggestions, rewarding accepted suggestion length while penalizing every acceptance, every suggestion shown and, most heavily, every dismissal."
---

The developer happiness metric ("счастье разработчика") is a composite metric for inline code suggestions proposed by the team behind [[SoftwareApplication/yandex-code-assistant]], as described in [[BlogPosting/how-we-taught-yandex-code-assistant-to-make-developers-happy]]. It scores a set of suggestions by the total length of accepted suggestions, minus a fixed penalty for each acceptance, minus a small penalty proportional to the length of every suggestion shown, minus a large penalty for each dismissal. The team's "formula v1.0" writes this as Σ(AcceptedLength − 3·NumAccepts) − 0.05·ΣShowSuggestLength − 14·ΣNumDiscards.

## Usage

The metric was introduced as a replacement for acceptance rate — the ratio of accepted suggestions to suggestions seen — after the team observed acceptance rate rising while its audience left. The post's diagnosis is that acceptance rate ignores the length of what is accepted and can be inflated by showing many short suggestions that are easy to accept in place of one long one. The happiness metric encodes four stated premises instead: a longer accepted suggestion is better; pressing Tab is itself effort, so short suggestions that would be quicker to type should not pay off; every suggestion shown is a distraction that has to be read, whatever the user then does; and a dismissal is explicit negative feedback that also costs an extra keystroke, so it is penalized most.

## When It Applies

It is a single team's metric for one product, not an established measure, and its evidence is that team's own. The coefficients were fitted by linear optimization over samples from earlier online A/B experiments whose winners were already known, optimizing the logarithm of the difference between winner and loser so that small differences would reach significance faster; the team reports that every winner–loser pair was then called correctly and significantly, and that after switching to it, retention — the business metric it was meant to track — rose sharply even though acceptance rate initially fell. It assumes an online setting with enough traffic to run A/B tests, which the team obtained by splitting experiments by request rather than by user. The post's broader caveat is that any acceptance metric deserves doubt and may need to be changed again.

## Related Terms

[[DefinedTerm/ai-assisted-programming]]
