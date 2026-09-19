---
title: "The Anatomy of Harness Engineering: How to Evaluate, Iterate, and Guard AI Coding Agents"
type: "schema:BlogPosting"
lang: en
sources:
  - type: url
    url: 'https://developers.googleblog.com/the-anatomy-of-harness-engineering-how-to-evaluate-iterate-and-guard-ai-coding-agents/'
    hash: sha256:b7703e83eb963ad1264b1927a931ffc37279d57efe136cc6d02e664b3df6aa63
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [evaluation, harness-engineering, agents, agent-architecture]

properties:
  description: "A Google for Developers post arguing that behavioral evaluations — assertions on an agent's discrete intermediate actions — are a better iteration partner than end-to-end benchmarks when engineering an agent harness."
  author: ["Taylor Mullen", "Christian Gunderman"]
  datePublished: "2026-09-09"
  publisher: "[[Organization/google]]"
---

A Google for Developers post arguing that teams engineering an agent harness should
complement end-to-end benchmarks with [[DefinedTerm/behavioral-evaluation]] — assertions
on discrete, observable actions the agent takes rather than on whether it completed a
whole task. The authors open with a failure they say developers new to
[[DefinedTerm/harness-engineering]] repeatedly fall into: running benchmarks such as
Terminal-Bench and DeepSWE, watching a composite score move by a few percentage points,
and having no idea why it changed.

Their position is not that end-to-end benchmarks are wrong but that they are the wrong
instrument for iteration. The post describes behavioral evaluations as integration tests
for harness operation, sets out when in a project's life evaluations start being worth
running, gives an architecture and a worked assertion, and closes by arguing the two kinds
of evaluation are complementary rather than substitutes.

## Key Points

- The authors argue behavioral evaluations are often a better measure of confidence than
  end-to-end benchmarks: they show whether expected behaviours actually occur and whether
  a change is progress or a regression, and can serve as an iteration partner that gives
  insight into why a change moved the needle.
- They frame the contrast as report cards versus behavioral guideposts — most teams
  evaluate an agent like a student sitting an exam, and when the score drops, end-to-end
  benchmarks do not typically answer directly whether the model got overconfident on an
  ambiguous prompt, forgot to verify the test suite, or hallucinated a CLI flag.
- A behavioral eval asserts on intermediate execution steps such as specific tool calls or
  file modifications rather than on final string equality. Their worked example asserts
  that an agent asked about live weather consulted a web-search tool rather than answering
  from memory.
- On timing, they argue evaluations belong to a second phase. A team bootstrapping an agent
  starts with developer instinct and dogfooding, and until the agent can dogfood its own
  codebase the authors say it does not make sense to run evaluations at all.
- They state the primary purpose of an evaluation suite is not to celebrate making the
  agent 2% better but to give confidence that a prompt tweak, tool schema change or model
  upgrade did not make it holistically worse.
- The recommended architecture separates behavioral assertions into fast, deterministic,
  unit-style checks that run locally — their illustration runs a local behavioural suite in
  under five seconds.
- They suggest a rich suite enables automated prompt engineering: an LLM tweaks its own
  system prompt until a failing test passes, with the rest of the suite acting as a
  CI/CD-style guardrail against breaking existing features.
- Their three-step starting loop is to pick one failure mode from a mistake the agent
  actually made; write assertions matched to task complexity — strict single-turn
  assertions for simple tasks with one optimal solution, and fuzzier outcome-based checks
  such as [[DefinedTerm/llm-as-a-judge]] for complex tasks where the model may take an
  unexpected but correct path; and automate batch evaluations rather than blocking pull
  requests on single noisy runs, tracking aggregate pass rates over time.
- The closing argument is that the two kinds are complementary: macro benchmarks verify the
  final destination while micro behavioral evals enable safe, rapid iteration, and the
  recommendation is to adopt both.

## Context

This is a Google engineering team's account of its own practice, published on Google's own
developer blog, and its worked example is written against Google's own Antigravity SDK. It
reports no comparative measurement of behavioral evaluation against end-to-end
benchmarking — the case is made from the authors' stated experience keeping agent systems
reliable as models evolve, not from a study.

The post's framing sits within the broader argument that an agent's scaffolding, rather
than its model, is the main object of engineering — see
[[DefinedTerm/harness-engineering]]. Its recommendation to treat the harness as standard
software requiring unit and integration testing connects it to
[[DefinedTerm/verification-loop]] and to work on [[DefinedTerm/guardrails]].
