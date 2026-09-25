---
title: "pass@k"
type: "schema:DefinedTerm"
lang: en
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
  description: "An evaluation metric giving the likelihood that an agent or model produces at least one correct solution in k attempts at a task."
---

pass@k is an evaluation metric that measures the likelihood that an agent gets at least one correct solution in *k* attempts at a task. Because more attempts mean more chances of a success, the score rises as *k* increases. At *k* = 1 it equals the per-trial success rate: a pass@1 of 50% means the model succeeds at half the tasks in the eval on its first try.

## Usage

[[BlogPosting/demystifying-evals-for-ai-agents]] presents pass@k as one of two metrics for handling non-determinism in agent evaluation, where the same task may pass on one run and fail on the next. It notes that in coding the main interest is often in the agent finding the solution on the first try — pass@1 — while in other cases proposing many solutions is acceptable as long as one of them works. The same post recommends pass@k for tools where one success matters, and its counterpart [[DefinedTerm/pass-hat-k]] for agents where consistency is essential; as trials increase the two diverge, and by *k* = 10 pass@k approaches 100% while pass^k falls toward 0%.

The post also uses the metric to read eval results: with frontier models, a 0% pass rate across many trials — its example is 0% pass@100 — is described as most often a sign of a broken task rather than an incapable agent.

## Related Terms

[[DefinedTerm/pass-hat-k]], [[DefinedTerm/trajectory-evaluation]]
