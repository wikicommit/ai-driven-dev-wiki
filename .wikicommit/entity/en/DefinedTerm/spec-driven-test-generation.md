---
title: "Spec-Driven Test Generation"
type: "schema:DefinedTerm"
lang: en
tags: [spec-driven-development, agents]
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
  description: "A test-generation technique in which an LLM-based agent is instructed to first reason about and explicitly document the code's pre-conditions, post-conditions and undefined behaviours, and to use that intermediate semi-formal specification as a scaffold for the tests it then writes."
---

Spec-driven test generation is a way of prompting an LLM-based coding agent to write tests: rather than asking for tests directly, the agent is instructed first to reason about — and explicitly document — the code's pre-conditions, post-conditions and undefined behaviors. The resulting intermediate, semi-formal specification is then used as what its proposers call a cognitive scaffold to guide the test generation that follows. The term is proposed in [[ScholarlyArticle/grounding-ai-agents-in-contracts]].

## Usage

What the technique adds is an artifact: a description of the code's contract, produced and written down before any test is. Its motivation is a failure attributed to direct prompting — that an agent asked straight for tests can fail to reason about the code and its underlying contracts, and so miss edge cases and behavioral boundaries that bear on test quality.

## When It Applies

It is proposed for agentic test generation against existing code, and evaluated in that setting on production bugs from Google, where the reported gains over a conventional test-generation agent are 9.8 percentage points of bug detection rate and 2.5 percentage points of branch coverage. A model-judged comparison is reported to prefer its suites in 77.8% of cases against that baseline, and in 56.7% of cases against human-authored tests.

What the term names here is specific: the specification is written by the agent, about code that already exists, and serves to ground the tests generated from it rather than to drive an implementation. See [[DefinedTerm/spec-driven-development]] for the broader practice that the proposing paper's venue places this in.

## Related Terms

[[DefinedTerm/spec-driven-development]], [[DefinedTerm/llm-as-a-judge]], [[DefinedTerm/test-design]], [[DefinedTerm/characterization-test]]
