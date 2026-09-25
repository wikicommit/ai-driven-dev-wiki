---
title: "pass^k"
type: "schema:DefinedTerm"
lang: en
aliases: ["pass-hat-k"]
tags: [agent-evaluation, evals]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents'
    hash: sha256:aff580d13a3f50486ad4c230339a558e501350b4038901e8093333bdd7842ca9
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An evaluation metric giving the probability that all k trials of a task succeed, used to measure how consistently an agent performs."
---

pass^k is an evaluation metric that measures the probability that *all k* trials of a task succeed. Because demanding consistency across more trials is a harder bar to clear, the score falls as *k* increases. At *k* = 1 it equals the per-trial success rate; for an agent with a 75% per-trial success rate, the probability of passing all of three trials is (0.75)³ ≈ 42%.

## Usage

[[BlogPosting/demystifying-evals-for-ai-agents]] presents pass^k alongside [[DefinedTerm/pass-at-k]] as a way to capture the non-determinism of agents, whose behavior varies between runs. It argues that pass^k matters especially for customer-facing agents, where users expect reliable behavior every time, and recommends it for agents where consistency is essential, while pass@k suits tools where a single success is enough. The two metrics are identical at *k* = 1 and diverge as trials increase: by *k* = 10, pass@k approaches 100% while pass^k falls toward 0%.

For its definition of the metric the post links to the same paper it cites for [[Dataset/tau-bench]], a benchmark simulating multi-turn conversations in domains such as retail support and airline booking.

## Related Terms

[[DefinedTerm/pass-at-k]], [[Dataset/tau-bench]]
