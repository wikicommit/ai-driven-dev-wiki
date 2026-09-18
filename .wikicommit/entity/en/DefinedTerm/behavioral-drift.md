---
title: "Behavioral Drift"
type: "schema:DefinedTerm"
lang: en
tags: [agents, evaluation, governance]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.28791'
    hash: sha256:0de559cacdfe9078d48a08a5f2b05d76219a579abd307e3a72ca17d1894464d0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The degradation of an agentic system over time through shifts in its input distribution, in the relationship between inputs and correct outputs, and through provider-side model updates — so that the system has no stable terminal state and requires permanent stewardship."
---

Behavioral drift is the term [[ScholarlyArticle/from-determinism-to-delegation]] uses for the way
agentic systems degrade, which it sets against deterministic software as the thing that does not. The paper separates two distributional shifts. **Data drift** is a shift in the marginal
input distribution: the inputs the system meets in production stop resembling those it was trained on.
**Concept drift** is a shift in the conditional: the same input should now produce a different correct
output. The paper states the two separately without commenting on how they relate.

The paper names a further cause alongside those two. Because the underlying model may also be updated
by its provider, an agent can change behaviour without anything in its own deployment changing. The consequence the paper draws is that an agent has no stable terminal state and requires
permanent stewardship together with automated statistical monitoring under testing, evaluation,
verification and validation regimes.

## Usage

The concept is used to argue that "done" is not a meaningful state for an agentic system. In that
paper's fourteen-dimension comparison it is what the lifecycle row turns on: classical practice runs
spec, design, implement, test and deploy toward a clear "done", while agentic practice is
experiment-heavy and trace-driven with no terminal "done", because behaviour drifts.

It is worth reading beside [[DefinedTerm/compositional-reliability]], which the same paper treats in
the adjacent section: that one concerns how far an agent can be trusted within a single long run, this
one how long any measurement of it stays valid. The paper discusses both among the mechanisms
underlying autonomous software agents; the pairing here is this wiki's, not a grouping the paper makes.

## When It Applies

The paper states the contrast as agentic systems degrading through drift where deterministic software
does not. The provider-update case widens that further: it applies even
where the deploying organisation changes nothing at all, which is what makes it a governance concern
rather than only an engineering one.

What it demands, in the paper's terms, is permanent stewardship and automated statistical monitoring
rather than a test suite that passes or fails, because the thing being watched is a distribution rather than a value. The paper connects
this to its treatment of evaluation as the central artifact of agentic practice, and specifically to
robustness being quantified through frameworks that exceed static accuracy and evaluate reaction to
data, model and intent drift.

Its consequences reach the paper's open problems from two directions. Under sustained stewardship, it
states that the cost model of permanent monitoring, re-evaluation and re-alignment is not yet well
understood at the portfolio level. Under accountability attribution, it names vendor-supplied model
updates that silently alter behaviour as part of what makes responsibility allocation legally and
ethically unsettled — the drift is not merely a reliability problem but a question of who is answerable
when a system changes underneath its operator.

This account rests on one position paper, which states the two distributional shifts and the
provider-update cause compactly and draws its conclusion from them jointly. It reports no measurement
of drift of its own.

## Related Terms

- [[ScholarlyArticle/from-determinism-to-delegation]] — the paper this account is drawn from
- [[DefinedTerm/compositional-reliability]] — the adjacent mechanism the same paper treats, on a
  different time axis
- [[DefinedTerm/context-rot]] — a distinct within-session degradation, not this cross-time one
- [[DefinedTerm/ai-native-software-engineering]] — the paradigm in which permanent stewardship replaces
  a terminal "done"
