---
title: "Self-Repair"
type: "schema:DefinedTerm"
lang: en
tags: [code-generation, self-correction, execution-feedback]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2306.09896'
    hash: sha256:17363bf30fafe6de7a50c6774def21c41d9bd0ed6d6b439b18b524bcd6f343ff
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A technique for LLM code generation in which the model introspects on and corrects mistakes in its own code: a generated program is run against unit tests, and on failure the error message and faulty program are turned into feedback from which a repaired program is generated."
---

Self-repair is a technique for improving code generation with large language models in which the model introspects and corrects mistakes in its own code. In the typical workflow described in [[ScholarlyArticle/is-self-repair-a-silver-bullet-for-code-generation]], a program is sampled from a code generation model and run against a suite of unit tests provided as part of the specification; if it fails any test, the error message and faulty program are given to a feedback model that explains why the code failed, and that feedback is passed to a repair model that generates a fixed version. The feedback and repair steps can be carried out in a single interaction with the same model, but treating them as separate stages makes it possible to study the feedback on its own.

## Usage

The term is used in research on LLM code generation for approaches that add a debugging and repair loop after initial generation, instead of only sampling more candidate programs. The paper above presents self-repair as having recently become a popular way to boost performance on complex coding tasks, and lists as its appeal that it can overcome mistakes caused by unlucky samples during decoding, easily incorporates feedback from symbolic systems such as compilers, static analysis tools and execution engines, and mimics the trial-and-error way human software engineers write code. The same paper notes that self-repair has also been used outside code generation, for example to mitigate hallucinations in search assistants.

## When It Applies

Self-repair as studied in that paper assumes a specification with executable unit tests, so that a failing program produces an error message or a mismatching example to repair against; the authors point out that real-world development differs, with incomplete specifications, long contextual dependencies and tests that are unlikely to exist for each snippet. Its main cost is that it needs more model invocations, so whether it pays off depends on whether the same budget spent on drawing more independent samples would have done better. Their measurements with CodeLlama-13b-instruct, GPT-3.5 and GPT-4 on HumanEval and APPS found the gains often modest and inconsistent once this cost is counted, larger when the budget goes to diverse initial programs rather than repeated repairs, and limited mainly by the quality of the model's feedback on its own code — stronger-model or human feedback improved repair substantially. These findings come from one study on self-contained Python problems rather than a settled consensus.

## Related Terms

- [[DefinedTerm/human-in-the-loop]]
