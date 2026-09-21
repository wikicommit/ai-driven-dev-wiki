---
title: "Grounding AI Agents in Contracts: An Empirical Evaluation of Spec-Driven Test Generation"
type: "schema:ScholarlyArticle"
lang: en
tags: [spec-driven-development, agents, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2608.17177'
    hash: sha256:b59cbddfb96da6a622e05cf57866bcb6a48fcbb4c17181a7340313aaad77af70
    license: CC-BY-4.0
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An empirical evaluation of Spec-Driven Test Generation, in which a coding agent is made to document a unit of code's pre-conditions, post-conditions and undefined behaviours before writing tests for it, reported to improve bug detection and branch coverage over a conventional test-generation agent on production bugs from Google."
  author: ["Michele Tufano", "James McClure", "José Cambronero", "Runxiang Cheng", "Sherry Y. Shi", "Renyao Wei", "Dorothy Chen", "Franjo Ivančić", "Livio Dalloro", "Pat Rondon"]
  datePublished: "2026-08-17"
  abstract: "The paper observes that LLM-based agents prompted directly to generate tests can fail to reason about the code and its underlying contracts, missing edge cases and behavioral boundaries that affect test quality. It proposes instructing the agent to first reason about and explicitly document pre-conditions, post-conditions and undefined behaviors, using that semi-formal specification as a cognitive scaffold for the test generation that follows, and evaluates the result on production bugs from Google."
  keywords: ["Spec-Driven Test Generation", "Test Generation", "LLM-based Agents", "Software Engineering"]
---

This paper proposes and evaluates **Spec-Driven Test Generation**, an intervention in how a coding agent is prompted for test generation. Its starting observation is that LLM-based agents, though they have outperformed many classical approaches and scaled to repository-level tasks such as test generation, can fail to reason about the code and its underlying contracts when asked directly for tests — missing edge cases and behavioral boundaries that affect test quality. The proposed remedy is an intermediate step: instruct the agent first to reason about, and explicitly write down, the code's pre-conditions, post-conditions and undefined behaviors, and let that semi-formal specification act as what the authors call a cognitive scaffold for the test generation that follows.

The evaluation is on production bugs from Google, comparing the spec-driven agent against a traditional test-generation agent baseline, and is reported on two automatic measures plus a model-judged qualitative comparison. The paper is to appear in the Proceedings of the 1st International Workshop on Specification-Driven Development Life Cycle (SpecOps 2026), co-located with SPLASH 2026. It was submitted on 17 August 2026 and last revised on 21 August 2026 (v2, the version summarized here). It carries the arXiv DOI 10.48550/arXiv.2608.17177 and a related DOI at 10.1145/3842652.3843195, and is released under CC BY 4.0.

## Key Points

- The stated failure mode being addressed is that an agent prompted directly for tests can fail to reason about the code and its underlying contracts, missing edge cases and behavioral boundaries.
- The proposed method has the agent produce an explicit intermediate artifact — documented pre-conditions, post-conditions and undefined behaviors — before generating tests.
- On production bugs from Google, the spec-driven agent is reported to deliver a 9.8 percentage point improvement in bug detection rate, with a reported p-value of 0.0352.
- On the same evaluation it is reported to deliver a 2.5 percentage point improvement in branch coverage, with a reported p-value of 0.0034.
- Using [[DefinedTerm/llm-as-a-judge]], the paper reports its test suites judged superior to the baseline's in 77.8% of cases and superior to human-authored tests in 56.7% of cases.
- The judged improvements are reported along three named dimensions: following best practices, readability, and edge-case coverage.
- Both the effect sizes and the judged comparisons rest on one evaluation set — production bugs from a single organization — and the qualitative comparison is model-judged rather than human-judged.

## Notes

The paper's venue places it in the [[DefinedTerm/spec-driven-development]] line of work: it is to appear at a workshop dedicated to the specification-driven development life cycle. What the abstract itself sets out is specific — the specification is produced by the agent, about code that already exists, and its purpose is to ground the tests the agent then writes.
