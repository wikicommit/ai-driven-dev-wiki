---
title: "SpecGen: Automated Generation of Formal Program Specifications via Large Language Models"
type: "schema:ScholarlyArticle"
lang: en
tags: [formal-specification, program-verification, code-generation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2401.08807'
    hash: sha256:6a6004213a4b820907bab2aba7366b089e0ffbc10ea7d98d01378dd2d970b075
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper introducing SpecGen, an LLM-based technique for generating formal JML specifications for Java programs, which combines a conversation that feeds verifier failures back to the LLM with a mutation-based phase that repairs failed specifications. It generated verifiable specifications for 279 of 385 programs, more than the LLM-based and template-based baselines it was compared with."
  author: ["Lezhi Ma", "Shangqing Liu", "Yi Li", "Xiaofei Xie", "Lei Bu"]
  keywords: ["program verification", "specification inference", "large language model", "JML"]
---

The paper addresses the lack of documented formal specifications — pre- and post-conditions, loop invariants and assertions — in most real-world software, which it attributes to how hard such specifications are to write by hand. Existing automated tools such as Houdini and Daikon generate candidate specifications from templates defined by human experts; the authors argue this yields overly simplistic specifications that cannot capture the behaviour of complex programs. SpecGen instead uses the code comprehension ability of large language models to generate specifications in the Java Modeling Language (JML), checked with the OpenJML verifier.

SpecGen works in two phases. In conversation-driven specification generation, a prompt built from a system role, few-shot examples and the queried program asks the LLM for JML specifications; each output is verified, and a failure produces a feedback prompt carrying the verifier's error message, plus natural-language guidance for common failure types, for the next round, up to a maximum number of rounds. Observing that failed LLM output is often already close to the correct specification, the authors add a mutation-based phase for programs where the conversation fails: four kinds of mutation operators — predicative, logical, comparative and arithmetic — substitute operators in the failed specifications to produce candidate variants, and a heuristic selection strategy assigns weights to mutation types and prefers candidates with fewer mutations when choosing which variants to verify.

## Key Points

- SpecGen generated verifiable specifications for 279 of 385 programs across the SV-COMP Java benchmark (265 programs) and the authors' [[Dataset/specgenbench]] (120 programs), against 247 for AutoSpec, 218 for the conversational approach alone, 98 for Houdini and 72 for Daikon.
- Its average success probability over 10 trials per program was 59.97%, against 46.13% for AutoSpec and 35.95% for conversational generation.
- An ablation found every mutation type contributes, with comparative mutation contributing most — disabling it reduced the handled programs to 223 — which the authors attribute to the recurring need to bound numerical and loop variables.
- The heuristic selection strategy reduced the average number of verifier calls on SpecGenBench from 36.20 to 28.51 compared with random selection (a 21.23% improvement), and only modestly on SV-COMP.
- In a user study with 15 Ph.D. students on 15 programs, SpecGen's specifications averaged a rating of 4.54 out of 5, close to the ground-truth specifications' 4.83 and well above the 2.32 of Houdini and Daikon.
- On 50 Java files from nine Defects4J repositories, SpecGen handled 38, against 28 for the conversational approach and 15 for Daikon.

## Notes

The experiments used gpt-3.5-turbo-1106. The authors note that SpecGen performs relatively poorly on programs with nested loops, that OpenJML's implementation flaws may cause some correct specifications to fail verification, and that part of their data (20 programs from an existing dataset and SV-COMP) carries a data leakage risk, although SpecGen still handled 87 of the remaining 100 programs. They also found that 88.7% of the SV-COMP programs they used are loop-free, which motivated building SpecGenBench.
