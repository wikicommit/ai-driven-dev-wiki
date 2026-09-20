---
title: "Multi-SWE-bench: A Multilingual Benchmark for Issue Resolving"
type: "schema:ScholarlyArticle"
lang: en
tags: [evaluation, coding-agents, llm, software-engineering, reinforcement-learning]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2504.02605'
    hash: sha256:efffadb8771463b26f920f9ded479e505f88487063add19a6bfb5eafcc304e4e
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint that introduces Multi-SWE-bench, a multilingual issue-resolving benchmark spanning seven languages beyond Python, and launches the Multi-SWE-RL community for building reinforcement-learning training data for the same task."
  author: ["Daoguang Zan", "Zhirong Huang", "Wei Liu", "Hanwu Chen", "Linhao Zhang", "Shulin Xin", "Lu Chen", "Qi Liu", "Xiaojian Zhong", "Aoyan Li", "Siyao Liu", "Yongsheng Xiao", "Liangqiang Chen", "Yuyu Zhang", "Jing Su", "Tianyu Liu", "Rui Long", "Kai Shen", "Liang Xiang"]
  datePublished: "2025-04-03"
  abstract: "The paper defines issue resolving as modifying a codebase to generate a patch that addresses a given issue, and observes that existing benchmarks such as SWE-bench focus almost exclusively on Python, making them insufficient for evaluating LLMs across diverse software ecosystems. It introduces Multi-SWE-bench, covering Java, TypeScript, JavaScript, Go, Rust, C and C++, with 1,632 high-quality instances annotated from 2,456 candidates by 68 expert annotators. Using it, the authors evaluate state-of-the-art models with three representative methods — Agentless, SWE-agent and OpenHands — and present an analysis with empirical insights. They also launch the Multi-SWE-RL open-source community for building large-scale RL training datasets, releasing 4,723 well-structured instances across seven languages and open-sourcing the entire data production pipeline with tutorials."
  keywords: ["Software Engineering (cs.SE)", "Artificial Intelligence (cs.AI)", "Computation and Language (cs.CL)"]
  citation: "arXiv:2504.02605, DOI 10.48550/arXiv.2504.02605"
---

This arXiv preprint addresses a gap it identifies in how issue-resolving systems are measured. It
defines the task first — the task of issue resolving is to modify a codebase to generate a patch
that addresses a given issue — and then states the problem: existing benchmarks, of which the
authors name [[Dataset/swe-bench]] as an example, focus almost exclusively on Python, which the
authors argue makes them insufficient for evaluating large language models across diverse software
ecosystems.

Its answer is [[Dataset/multi-swe-bench]], a multilingual issue-resolving benchmark covering Java,
TypeScript, JavaScript, Go, Rust, C and C++. The paper gives both its scale and how that scale was
arrived at: 1,632 high-quality instances, carefully annotated from 2,456 candidates by 68 expert
annotators, which the authors offer as the reason the benchmark can provide an accurate and reliable
evaluation.

On that basis the authors evaluate a series of state-of-the-art models using three representative
methods, which they name as [[DefinedTerm/agentless]], [[SoftwareApplication/swe-agent]] and
[[SoftwareApplication/openhands]], and present what they describe as a comprehensive analysis with
key empirical insights.

The paper's second contribution shifts from evaluation to training. The authors launch a
[[Dataset/multi-swe-rl]] open-source community, aimed at building large-scale reinforcement learning
training datasets for issue-resolving tasks, and as an initial contribution release a set of 4,723
well-structured instances spanning seven programming languages. They also open-source the entire
data production pipeline along with detailed tutorials, framing this as an encouragement for the
open-source community to continuously contribute and expand the dataset. The authors close by
envisioning Multi-SWE-bench and the growing Multi-SWE-RL community as catalysts for advancing
reinforcement learning toward its full potential.

The preprint is filed under Software Engineering (cs.SE), with cross-listings to Artificial
Intelligence (cs.AI) and Computation and Language (cs.CL). It was submitted on 3 April 2025 and
carries the arXiv-issued DOI 10.48550/arXiv.2504.02605.

## Key Points

- The paper's stated problem is that existing issue-resolving benchmarks focus almost exclusively on Python, which the authors argue makes them insufficient for evaluating LLMs across diverse software ecosystems.
- It introduces Multi-SWE-bench, covering seven languages beyond Python: Java, TypeScript, JavaScript, Go, Rust, C and C++.
- The benchmark's 1,632 instances were annotated from 2,456 candidates by 68 expert annotators, which the authors present as what makes the evaluation accurate and reliable.
- The authors evaluate state-of-the-art models on it using three representative methods — Agentless, SWE-agent and OpenHands — and report a comprehensive analysis with key empirical insights.
- They launch the Multi-SWE-RL open-source community for building large-scale RL training datasets for issue resolving, releasing 4,723 well-structured instances across seven programming languages as an initial contribution.
- The entire data production pipeline is open-sourced with detailed tutorials, with the stated aim of letting the community continuously contribute and expand the dataset.

## Notes

The paper carries two contributions with different purposes — an evaluation benchmark and a training
data effort — and links them through a shared task definition and a shared production pipeline. The
authors present the released pipeline, rather than the released instances alone, as what makes the
second contribution extensible. The claim about existing benchmarks is stated at the level of
language coverage; the paper's own numbers describe Multi-SWE-bench and the initial Multi-SWE-RL
release, not the benchmarks it contrasts itself with.
