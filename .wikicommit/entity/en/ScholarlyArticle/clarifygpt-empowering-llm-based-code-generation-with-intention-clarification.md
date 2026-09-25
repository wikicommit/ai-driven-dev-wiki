---
title: "ClarifyGPT: Empowering LLM-based Code Generation with Intention Clarification"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-generation, requirements-clarification, prompting]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2310.10996'
    hash: sha256:c40f7867a7252f0648e41055936bb4885a69af0bab81a96a32c92818f75ffc8c
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper introducing ClarifyGPT, a framework that lets an LLM detect ambiguous code-generation requirements through a code consistency check, ask targeted clarifying questions, and generate code from the refined requirement, improving Pass@1 for GPT-4 and ChatGPT across four benchmarks."
  author: ["Fangwen Mu", "Lin Shi", "Song Wang", "Zhuohao Yu", "Binquan Zhang", "Chenxue Wang", "Shichao Liu", "Qing Wang"]
  keywords: ["code generation", "ambiguous requirements", "clarifying questions", "user simulation"]
---

The paper argues that requirements written by users for code generation are inevitably sometimes ambiguous or insufficient, and that current LLMs generate programs from them directly rather than asking for clarification, so the result is likely to deviate from what the user intended — unlike human developers, who typically ask clarifying questions. It identifies two barriers to giving LLMs this ability: deciding *when* to ask, since questioning well-defined requirements wastes the user's time, and deciding *what* to ask, since vague questions invite off-topic answers.

ClarifyGPT addresses both in four stages. **Test input generation** prompts an LLM for seed inputs and then applies type-aware mutation to produce many more. **Code consistency check** samples several code solutions for the requirement, runs them on those inputs, and treats the requirement as ambiguous if their outputs differ, on the assumption that a clear requirement yields solutions that behave the same. **Reasoning-based question generation** has the LLM compare the inconsistent solutions, analyse what makes the requirement ambiguous, and then formulate targeted questions — an approach the authors liken to chain-of-thought prompting. **Enhanced code generation** appends the question-and-answer pairs to the requirement's docstring and generates the final code from the refined requirement. For evaluation without human participants, the authors also propose a user-simulation method that gives an LLM the clarifying questions together with the ground-truth test cases so that it can answer in the user's place.

## Key Points

- ClarifyGPT decides whether to ask questions at all by checking whether sampled solutions agree on generated test inputs, so an unambiguous requirement goes straight to code generation without any questions.
- In a human evaluation with ten participants answering the generated questions, ClarifyGPT raised GPT-4's Pass@1 on MBPP-sanitized from 70.96% to 80.80% and on MBPP-ET from 51.52% to 60.19%.
- With simulated user feedback, it improved GPT-4's average Pass@1 across HumanEval, HumanEval-ET, MBPP-sanitized and MBPP-ET from 68.02% to 75.75%, and ChatGPT's from 58.55% to 67.22%.
- It outperformed the Default, chain-of-thought and GPT-Engineer baselines in these experiments; the authors attribute the margin over GPT-Engineer, which asks clarifying questions for every requirement, to identifying ambiguous requirements first and asking targeted questions.
- Performance with simulated feedback was slightly below that with human feedback, which the authors read as the simulation sometimes producing answers that do not match the user's intent, while still supporting its use as a proxy.
- Performance rose with the number of demonstrations in the prompt from zero to three, with the one-shot setting already close to three-shot.

## Notes

The authors note two limitations: the framework needs LLMs with enough instruction-following ability to ask questions, ruling out models without instruction tuning, and because it relies on comparing test outputs it is not suited to code with complex inputs such as images or files, or code that returns no output value. They identify possible data leakage from public benchmarks and the fidelity of simulated users as threats to validity. The paper is dated October 2023 and the authors are affiliated with the Institute of Software, Chinese Academy of Sciences, Beihang University, York University and Huawei.
