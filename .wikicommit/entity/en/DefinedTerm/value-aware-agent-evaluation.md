---
title: "Value-Aware Agent Evaluation"
type: "schema:DefinedTerm"
lang: en
tags: [evaluation, benchmarking, agent-architecture, deployment]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.20683'
    hash: sha256:4d2fd9336c3ac20f51ab2d6d4fc4eb98e0ba0673a8d3475e0e286c3fdfc4511a
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An evaluation stance proposed by Guo et al. that ranks agent systems not by task success alone but by expected task value weighted by success probability and process quality, subject to cost, latency, risk and repeated-run reliability constraints."
---

Value-aware agent evaluation is the proposal, made in [[ScholarlyArticle/survey-on-agent-system-and-harness-design]], to move agent assessment from a score-centric ranking by task success to an objective that couples the value of a task with the cost, latency, risk and reliability of completing it. The survey observes that current agent leaderboards rank systems by task success while API cost, latency, safety and trace quality are secondary or missing, which it calls useful for frontier comparison but incomplete for deployment. In place of maximizing success alone it writes an optimization over the model and harness jointly: maximize the expected product of task utility, the success probability of that model–harness pair, and a summary of process quality, subject to bounds on expected cost, on a quantile of latency, on expected safety or compliance risk, and a floor on repeated-run reliability. The authors present this not as a universal leaderboard score but as a family of deployment-specific utilities that makes the deployment target explicit.

## Usage

The survey names five dimensions a richer reading of results should cover: task success, whether the final objective is completed; reliability, whether performance remains stable across stochastic runs, retries and environment variations; efficiency, in token usage and API or compute cost; latency, as wall-clock time or number of interactions; and process quality, whether the trajectory is inspectable, recoverable and evidence-backed. To these it adds safety, whether actions remain within allowed boundaries and avoid harmful side effects. Its argument for the set is that similar final scores can hide substantial harness differences: one harness may trade long trajectories, repeated retries and heavy context accumulation for higher success, while another delivers slightly lower success at much lower cost and latency.

A complementary formulation the survey gives is value density, in which task value multiplied by success and process quality is divided by a denominator combining normalized cost, latency and risk under tunable exponents — so that high-value tasks may tolerate stronger verification while high-frequency workflows penalize latency and cost. The same execution traces also support simpler reports such as cost per effective success or latency per successful task, which distinguish systems with similar success rates but different runtime profiles. From this perspective the survey describes harness engineering as a resource-allocation problem: model routing, context compression, cache reuse, verifier selection, recovery policy and early stopping determine useful progress per unit cost rather than being implementation details.

## When It Applies

This is a proposal for how agent evaluation should be conducted, put forward by one survey rather than an established reporting convention, and the survey frames it as a direction for future benchmarks. It presupposes that execution traces carry the needed fields — outcomes, cost, tool calls, retries, verifier signals, recovery attempts, policy violations — and the survey's own experience is that they often do not: in its Terminal-Bench analysis, reward, agent-runtime and full-runtime fields had high coverage while input and output token fields covered 45.0% of trial records and dollar-cost fields only 15.2%, which is why it declines to use monetary cost for cross-harness claims. Where trace fields are sparse or accounted for differently by each harness, the formulation cannot be instantiated and the survey falls back on success, runtime, timeout behaviour and token usage where available.

It is also stated as a stance rather than a fixed metric: the exponents and bounds are deployment choices, so two teams applying it to the same systems can reach different rankings by design. The survey's concrete recommendation, separable from the formalism, is that benchmark reports include model version, harness identity, tool privileges, retry and timeout policy, execution environment, token or API usage where available, and trace or verifier metadata — on the argument that a benchmark score is interpretable only together with the runtime configuration that produced it.

## Related Terms

- [[DefinedTerm/execution-harness]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/trajectory-evaluation]]
- [[DefinedTerm/behavioral-evaluation]]
- [[DefinedTerm/output-verifiability]]
