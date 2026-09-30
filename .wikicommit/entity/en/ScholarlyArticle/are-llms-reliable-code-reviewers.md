---
title: "Are LLMs Reliable Code Reviewers? Systematic Overcorrection in Requirement Conformance Judgement"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, llm-evaluation, reliability]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2603.00539'
    hash: sha256:5e3e321b6a175be713ab1a959f980eeca48efdc0fb8797e4d49aa5a2734a1c26
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A study showing that LLMs asked to judge whether code satisfies a natural-language requirement systematically misclassify correct code as non-compliant, that more detailed prompts asking for explanations and fixes make this worse, and proposing a Fix-guided Verification Filter that tests the model's proposed fix as counterfactual evidence."
  author: ["Haolin Jin", "Huaming Chen"]
  datePublished: "2026-02-28"
  keywords: ["LLM code review", "requirement conformance", "overcorrection", "prompt design", "verification"]
---

This paper asks whether LLMs can reliably judge whether a code implementation satisfies its task description, a check software engineers increasingly delegate to them. Using widely adopted benchmarks and a unified prompt design, the authors report a systematic failure: LLMs frequently misclassify correct implementations as non-compliant or defective — the "overcorrection" of the title.

The paper also finds that prompt design pushes the error in an unexpected direction: more detailed prompts, particularly those that require the model to give explanations and propose corrections, lead to higher misjudgment rates. The authors analyse the mechanisms behind these failures and evaluate how reliable rationale-required judgments are. As a remedy they propose a Fix-guided Verification Filter, which treats the fix a model proposes as executable counterfactual evidence and validates both the original and the revised implementation using benchmark tests and spec-constrained augmented tests.

## Key Points

- LLMs used to check code against natural-language requirements frequently label correct code as non-compliant or defective.
- More detailed prompts — especially ones requiring explanations and proposed corrections — produce higher misjudgment rates, not lower ones, which the authors present as a critical reliability issue for LLM-based code assistants.
- The proposed Fix-guided Verification Filter uses the model's own suggested fix as executable counterfactual evidence, validating both the original and revised implementations with benchmark tests and spec-constrained augmented tests.
- The authors frame their results as exposing under-explored limitations of LLM-based code review and as practical guidance for adding safeguards when LLM reviewers are integrated into automated review and development pipelines.

## Notes

The findings are drawn from widely adopted benchmarks with a unified prompt design. The paper bears on the use of LLMs as automated reviewers in [[DefinedTerm/agentic-code-review]] and on the reliability of model-based judging more generally, as in [[DefinedTerm/llm-as-a-judge]].
