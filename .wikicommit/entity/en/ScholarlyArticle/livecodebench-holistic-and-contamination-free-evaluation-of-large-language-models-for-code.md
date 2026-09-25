---
title: "LiveCodeBench: Holistic and Contamination Free Evaluation of Large Language Models for Code"
type: "schema:ScholarlyArticle"
lang: en
tags: [benchmark, code-generation, evaluation, data-contamination]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2403.07974'
    hash: sha256:67c28aaadc21ea0b54adf573ed254a4ee0e73c81cd2972017fa0c8f6974ef524
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The paper introducing LiveCodeBench, a continuously updated benchmark for code LLMs built from dated contest problems so that models can be evaluated only on problems released after their training cutoff, and covering self-repair, code execution and test output prediction as well as code generation. Evaluating 52 models, it reports evidence of contamination in some models and of HumanEval overfitting in fine-tuned open models."
  author: ["Naman Jain", "King Han", "Alex Gu", "Wen-Ding Li", "Fanjia Yan", "Tianjun Zhang", "Sida I. Wang", "Armando Solar-Lezama", "Koushik Sen", "Ion Stoica"]
  keywords: ["benchmark", "code generation", "data contamination", "self-repair", "code execution", "test output prediction"]
---

The paper argues that existing code benchmarks such as HumanEval, MBPP and APPS no longer suffice for assessing newer LLMs: they measure only natural-language-to-code generation, and they may be contaminated or overfit because their problems can appear in training data. The authors, from UC Berkeley, MIT and Cornell, propose [[Dataset/livecodebench]], built on four principles: live updates that collect new problems from weekly contests and tag them with release dates, so a model can be scored only on problems published after its cutoff; holistic evaluation across several code-related capabilities; high-quality problems and tests; and balanced problem difficulty.

Beyond code generation, the benchmark evaluates [[DefinedTerm/self-repair]] (fixing an incorrect program from execution feedback), code execution (predicting a program's output on an input) and a newly introduced test output prediction task (producing the expected output for a given input from the problem statement alone). The authors motivate this by pointing to pipelines such as [[ScholarlyArticle/code-generation-with-alphacodium]], which combine reasoning, test generation, code generation and self-repair to improve on direct generation. At the time of the paper the benchmark held 511 problems from LeetCode, AtCoder and CodeForces released between May 2023 and May 2024, and the authors evaluated 18 base and 34 instruction-tuned models.

## Key Points

- Time-segmented evaluation exposed likely [[DefinedTerm/data-contamination]]: DeepSeek models dropped sharply on LeetCode problems released after August 2023, GPT-4-O on those released since November 2023 (its stated cutoff), and Codestral on problems since February 2024, while performance was relatively stable over time on AtCoder problems.
- Model rankings were highly correlated across the four scenarios (over 0.88 for every pair), but relative gaps varied; Claude-3-Opus, for example, outperformed GPT-4-Turbo on test output prediction.
- Comparing HumanEval+ with the easy split of LiveCodeBench showed only a moderate correlation (0.72) and two clusters of models; the cluster that did well only on HumanEval+ consisted mainly of fine-tuned open-access models, which the authors interpret as likely overfitting to HumanEval.
- Closed API models such as GPT-4-Turbo, GPT-4, Gemini-Pro-1.5 and Claude-3-Opus led with wide margins, and only a few large instruction-tuned open models (L3-Ins-70B, Mixtral and DS-Ins-33B) approached them.
- Post-training improved code generation over the base models, and the authors conclude that strong base models combined with high-quality post-training data are a viable recipe for good code LLMs.
- GPT-4-Turbo gained notably from self-repair (24.5% to 36.9% on medium problems) while Gemini-Pro gained little (8.5% to 9.4%).

## Notes

The authors list as limitations the small evaluation set once contaminated time windows are excluded (349 problems, with an estimated 1–1.5% performance variation), a focus on Python only, prompts that were not tuned per model, and a problem domain limited to competition programming, which may not represent real-world, open-ended LLM use. They recommend using LiveCodeBench as a starting point alongside domain-specific evaluations, and plan to add more platforms and an unreleased private test set.
