---
title: "Compositional Reliability"
type: "schema:DefinedTerm"
lang: en
tags: [agents, evaluation, long-horizon-tasks]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.28791'
    hash: sha256:0de559cacdfe9078d48a08a5f2b05d76219a579abd307e3a72ca17d1894464d0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The multiplicative decay of an agent's end-to-end success probability over a sequence of dependent steps: a high per-step success rate compounds downward across a long horizon, which is why trajectory-level evaluation and human checkpoints govern usable autonomy rather than per-step accuracy."
---

Compositional reliability is the name
[[ScholarlyArticle/from-determinism-to-delegation]] gives to what it calls a distinctive and
underappreciated failure mode of agentic systems: the multiplicative decay of reliability over long
horizons. If an agent must complete n dependent steps and each step succeeds independently with
probability p, then under the independence assumption the end-to-end success probability is p raised to
the power n. The paper's own worked figure is that a seemingly strong per-step rate of p = 0.95 yields
only about 0.36 across twenty steps.

Two things make this more than arithmetic. The first is that the independence assumption is optimistic:
the paper is explicit that the formula is an upper bound in practice, because real errors are often
correlated and can cascade. The second is what follows from it for evaluation — that trajectory-level
evaluation, recovery and human checkpoints, rather than per-step accuracy alone, are what govern usable
autonomy.

## Usage

The concept is used to argue against reading per-step accuracy as a proxy for end-to-end capability
over a long horizon. It
gives a reason to prefer trajectory evaluation — asking whether the agent chose a correct sequence of
tools, even where the final answer varies — over scoring outcomes alone, and a reason to place human-in-the-loop
checkpoints on the consequential and destructive actions along the way, which is where the paper puts
them.

It is worth reading beside [[DefinedTerm/behavioral-drift]], which the same paper treats in the
adjacent section: drift concerns an agent having no stable terminal state over time, while
compositional reliability concerns the horizon within a single run. The paper discusses both among the
mechanisms underlying autonomous software agents; the juxtaposition here is this wiki's, not a grouping
the paper makes.

## When It Applies

The formula applies where the steps are genuinely **dependent** — where a later step requires an earlier
one to have succeeded — and where success at each step can be treated as having a probability at all.
It is least informative where steps are independent of one another, or where the agent can detect and
recover from a failed step — recovery breaks the chain the multiplication assumes, which is this wiki's
reading of why the paper names recovery as one of the three things that govern usable autonomy.

Its characteristic misuse is treating the bound as a prediction rather than a ceiling. Because errors
correlate in practice, the true figure is generally worse than p to the n, so the formula understates
the problem rather than overstating it. The formula also holds p fixed across every step, which a
heterogeneous task rarely satisfies — a limit of the model rather than one the paper states.

The paper lists bounding end-to-end reliability under correlated failures as an open problem, stating
that principled methods for doing so are needed — an acknowledgement that the independence formula is a
first approximation rather than a tool for planning. Beyond that formula and the consequences it draws
for evaluation, the paper offers no measurement of its own.

## Related Terms

- [[ScholarlyArticle/from-determinism-to-delegation]] — the paper that formalizes this for agentic
  systems
- [[DefinedTerm/behavioral-drift]] — the adjacent mechanism the same paper treats, on a different time
  axis
- [[DefinedTerm/trajectory-evaluation]] — the evaluation approach this result argues for
- [[DefinedTerm/human-in-the-loop]] — the checkpointing this result argues for
- [[DefinedTerm/ai-native-software-engineering]] — the paradigm this limit constrains
