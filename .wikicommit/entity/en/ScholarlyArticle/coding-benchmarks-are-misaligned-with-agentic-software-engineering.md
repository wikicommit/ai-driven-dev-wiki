---
title: "Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [benchmarking, evaluation, agent-harness, measurement-validity]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.17799'
    hash: sha256:98d0e3aebf3d1c5ab551f46a6c1f719389e820d2be1490bfefd669d87c107e69
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A position paper by researchers at Tessl arguing that coding benchmarks measure the wrong object: what is used in practice is a system harness, not a model, and current benchmarks collapse model, harness and environment into one end-to-end score. It sets out three symptoms of the misalignment and proposes a structural remedy for each."
  author: "Maria I. Gorinova, Macey Baker, Amy Heineike, Maksim Shaposhnikov, Rob Willoughby, Dru Knox"
  datePublished: "2026-07-18"
  abstract: "Coding agents have become a major mode of software engineering, but the benchmarks used to compare them were designed in a pre-agent era: they collapse model, harness and environment into a single end-to-end score, typically computed against one reference solution, with no component-level signal for iteration. The paper argues that current coding benchmarks are misaligned with agentic software engineering, because a coding agent in practice is not a model but a system harness — a composite of models, harnesses, contexts, environments and feedback signals, any one of which can move the benchmark score by margins comparable to those between adjacent model generations. It discusses three symptoms: benchmark scores conflate the model with the rest of the harness; grading against a single reference solution penalises equally valid alternatives; and the absence of signal at the level of individual harness components makes the end-to-end system score difficult to iterate on."
  citation:
    - "[[ScholarlyArticle/swe-bench-can-language-models-resolve-real-world-github-issues]]"
    - "[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]]"
---

This position paper argues that the benchmarks currently used to compare coding agents are misaligned with what agentic software engineering actually builds and runs. Its central claim is that a coding agent in practice is not a model but a [[DefinedTerm/system-harness]]: a composite of models, harnesses, contexts, environments and feedback signals, any one of which the authors say can move a benchmark score by margins comparable to those between adjacent model generations. Benchmarks such as SWE-bench, HumanEval, MBPP, LiveCodeBench and BigCodeBench are described as sharing one structure — a single model, a single harness and a single environment producing a single number — which the authors characterise as an end-to-end system score with no signal at the level of individual components, often compared against a single reference solution.

The method is argumentative rather than experimental: the authors read existing coding-agent evaluation work through the lens of the system harness they define, and draw throughout on [[SoftwareApplication/ns2]], an issue-driven system harness they built and open-sourced, as a concrete reference. They state that building and operating that harness surfaced many of the misalignments the paper articulates. The paper borrows measurement vocabulary from work on evaluating generative AI as a social-science measurement problem, distinguishing the construct (for example, "solves the bug") from its operationalisation, and uses that language to classify its own symptoms: the conflation of model and harness is presented as a discriminant-validity claim, and single-reference anchoring as a content-validity claim.

Its contribution is the three-symptom diagnosis together with a suggested structural remedy for each, and a call to action addressed to the community. Underneath all three the authors place the operationalisation gap, a term they take from Wallach et al. and apply to agentic coding: how to state what a coding system should do in terms an automated grader can apply, without prescribing how the agent should attempt it. They describe this as the hardest open problem inside the programme and the decisive constraint on the next generation of benchmarks.

## Key Points

- A coding agent in practice is a system harness rather than a model — an orchestration layer that turns higher-level goals into tasks, dispatches them to one or more agent harnesses, manages the environment and routes outputs through feedback. Practical agentic coding at scale operates at this level, while current coding benchmarks operate at the level of the agent harness.
- Benchmark scores conflate the model with the rest of the harness. The paper's Table 1 reproduces Terminal-Bench leaderboard entries for one fixed model across several agent harnesses, where accuracies range from roughly 58% to roughly 80%; since the model is fixed across the rows, the authors argue the spread cannot be explained as a difference in model capability. This rests on one leaderboard and one task distribution.
- Inference effort is named as an under-specified variable: some model APIs let the caller change the amount of inference compute used, so output quality can move even when the model name and agent code are nominally unchanged.
- Grading against a single reference solution mistakes both the construct and the grain. The authors argue an agent that resolves a flaky test by restating the API at a different level of abstraction is judged not on whether the bug is fixed but on whether the reference tests still hold, and that hidden unit tests cannot see what distinguishes good code from working code — abstraction choice, architectural fit, system design.
- The absence of component-level signal makes an end-to-end score hard to iterate on: it shows that something failed but not what to fix, so the improvement cycle degrades into intuition-guided ablation. The authors draw the analogy to unit versus integration testing in software.
- Feedback signals are categorised into three tiers by scope, latency and trust — inner loop (seconds to minutes: tests, types, lint, compile), middle loop (minutes to hours: reviewer requests, simulation, maintenance agents, score rubrics) and outer loop (days to weeks: PR acceptance, revert rate, incident reports, customer feedback) — crossed with a second axis distinguishing signals the harness can modify from those it cannot.
- Three suggested remedies are proposed, one per symptom: require harness-aware metadata at submission (model, agent harness version, environment hash, dataset version) plus at least one ablation across a non-model axis against a fixed baseline; replace single-reference-derived test sets with multi-shape behavioural verifiers such as property tests, reference oracles or differential tests; and treat the harness components as evaluation targets in their own right, reporting before/after deltas on scoped health metrics for maintenance agents rather than only whether the final pull request merged.
- The paper states its own alternative views and answers them, including "end-to-end scores reflect real usage" (the authors agree, and say they argue against using *only* end-to-end metrics) and "decomposed evaluations are too costly" (the authors claim the dominant cost in current practice is the opportunity cost of misattributing improvements).

## Notes

The paper positions itself alongside a body of work it reads as moving in the same direction: research that treats the harness or scaffold itself as the object of measurement, and work framing an agentic software engineering discipline in which passing tests alone is no longer treated as success. It presents its own argument as the measurement counterpart to that framing — if the artefact is a composite system, the benchmark must score the composite system.

As a position paper it offers no new experiment or dataset of its own; its evidence is a reading of published evaluation work plus the authors' experience operating their own harness, and the authors are explicit that the operationalisation problem underneath their three remedies remains open. The Terminal-Bench figures it reproduces are taken from that leaderboard rather than measured here, and the authors' claim about the size of harness-driven variance rests on that table together with cited practitioner reports.
