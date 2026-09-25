---
title: "Test Anchors"
type: "schema:DefinedTerm"
lang: en
tags: [code-generation, test-generation, execution-feedback]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2401.08500'
    hash: sha256:0b04951cf53383d9b58bed9fa05b768a2e74972e65c4ff2168ff413ff3d8ecd1
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A technique for iterating LLM-generated code against AI-generated tests, in which tests the code has already passed are kept as anchors and every later fix must still pass all of them, protecting against a wrong AI-generated test driving the code into an incorrect fix."
---

Test anchors are a technique, described in [[ScholarlyArticle/code-generation-with-alphacodium]], for running and fixing LLM-generated code against tests that the model itself generated and that may therefore be wrong. When such a test fails, it is unclear whether the code or the test is at fault, and the paper reports that asking the model directly "who is wrong" often produces hallucinations and can end in wrongly fixed code. With test anchors, iteration starts on the public tests, which are known to be correct, and every passed test becomes an anchor; the model then iterates on the AI-generated tests one by one, adding each passing test to the anchors and, when a test fails, assuming the code is wrong and fixing it — but requiring the fixed code to still pass all anchors acquired so far, so that the anchors protect against an incorrectly fixed code.

## Usage

The term comes from the AlphaCodium flow for competitive-programming code generation, where test anchors are used in the final stage that iterates on AI-generated tests. The authors add an optimization: sorting the AI-generated tests from easy to hard, so that the iterative process is more likely to acquire anchors early and use them as protection when iterating on the more complicated AI tests.

## When It Applies

Test anchors assume a starting set of tests known to be correct (the public tests), an executable environment in which generated code can be run against tests, and additional tests whose correctness is uncertain. The authors present the technique as a response to the fact that, even after double validation, some AI-generated tests will be wrong. It is one of several code-oriented design practices the AlphaCodium authors report finding beneficial in their own flow, evaluated on the CodeContests dataset; the paper does not report a separate measurement of the technique's individual contribution.

## Related Terms

- [[DefinedTerm/self-repair]]
