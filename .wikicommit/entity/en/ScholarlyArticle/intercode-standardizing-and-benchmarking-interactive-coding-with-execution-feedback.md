---
title: "InterCode: Standardizing and Benchmarking Interactive Coding with Execution Feedback"
type: "schema:ScholarlyArticle"
lang: en
tags: [benchmark, code-generation, execution-feedback]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2306.14898'
    hash: sha256:ac3e79408d398dfa7c56558d104f85928fcb3e0803df79bc3913041d361c2ffc
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A 2023 arXiv paper introducing InterCode, a framework that treats interactive coding as a standard reinforcement learning environment — code as actions, execution feedback as observations — and uses it to build Bash, SQL and Python benchmarks for evaluating LLMs."
  author: ["John Yang", "Akshara Prabhakar", "Karthik Narasimhan", "Shunyu Yao"]
  datePublished: "2023-06-26"
  keywords: ["InterCode", "interactive coding", "execution feedback", "reinforcement learning environment", "benchmark"]
---

This paper starts from the observation that humans write code interactively, relying on constant execution feedback to correct errors, resolve ambiguities and decompose tasks, whereas most coding benchmarks for LLMs treat coding as a static instruction-to-code transduction. The authors argue this static setup risks error propagation and disconnects generated code from the environment it will finally run in.

To close that gap they introduce InterCode, a lightweight framework that casts interactive coding as a standard reinforcement learning environment, with code as actions and execution feedback as observations. It is language- and platform-agnostic, runs in self-contained Docker environments for safe and reproducible execution, and is compatible with traditional sequence-to-sequence coding methods while supporting new methods for interactive code generation. The authors use it to build three interactive environments and evaluate several state-of-the-art LLMs on them.

## Key Points

- InterCode models interactive coding as a reinforcement learning environment in which code is the action and execution feedback is the observation.
- Execution happens in self-contained Docker environments, which the authors present as providing safe and reproducible execution.
- Three interactive code environments are built, with Bash, SQL and Python as action spaces, using data from the static NL2Bash, Spider and MBPP datasets.
- Multiple LLMs are evaluated with different prompting strategies, including [[DefinedTerm/react-prompting]] and Plan & Solve.
- The authors report that their results show the benefits of interactive code generation and that InterCode can serve as a challenging benchmark for code understanding and generation.
- The framework is described as easily extensible, for example to Capture the Flag tasks, which the paper characterizes as inherently multi-step and involving multiple programming languages.

## Notes

The paper was first submitted to arXiv on 26 June 2023 and last revised on 30 October 2023 (version 3). The authors publish code and data on a project site at <https://intercode-benchmark.github.io>.
