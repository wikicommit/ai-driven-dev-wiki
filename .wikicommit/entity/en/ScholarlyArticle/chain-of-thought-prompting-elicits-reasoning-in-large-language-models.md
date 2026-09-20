---
title: "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models"
type: "schema:ScholarlyArticle"
lang: en
tags: [prompt-engineering, llm, reasoning]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2201.11903'
    hash: sha256:ba5518784cf85c757b603addf8dffda10837f9e488c93b44ed9fdf5a380aae50
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint that introduces chain-of-thought prompting: supplying a few worked examples that show intermediate reasoning steps, which the authors report substantially improves large language models' performance on arithmetic, commonsense and symbolic reasoning tasks."
  author: ["Jason Wei", "Xuezhi Wang", "Dale Schuurmans", "Maarten Bosma", "Brian Ichter", "Fei Xia", "Ed Chi", "Quoc Le", "Denny Zhou"]
  datePublished: "2022-01-28"
  abstract: "The paper explores how generating a chain of thought — a series of intermediate reasoning steps — improves a large language model's ability to perform complex reasoning. It introduces chain of thought prompting, in which a few chain-of-thought demonstrations are supplied as exemplars in the prompt, and reports that such reasoning abilities emerge naturally in sufficiently large models. Experiments on three large language models show gains across arithmetic, commonsense and symbolic reasoning tasks."
---

This arXiv preprint introduces [[DefinedTerm/chain-of-thought]] prompting, a method in which a small
number of demonstrations showing intermediate reasoning steps are supplied as exemplars in a
prompt. The authors' claim is that generating such a chain of thought — a series of intermediate
reasoning steps — significantly improves a large language model's ability to perform complex
reasoning, and that this ability emerges naturally in sufficiently large models. The authors
describe chain of thought prompting as a simple method.

The evaluation reported in the abstract covers three large language models across arithmetic,
commonsense and symbolic reasoning tasks. The authors describe the empirical gains as striking and
give one headline result: prompting a 540B-parameter language model with just eight chain-of-thought
exemplars reaches state-of-the-art accuracy on the GSM8K benchmark of math word problems, surpassing
even a finetuned GPT-3 with a verifier.

The paper is filed under Computation and Language (cs.CL) and Artificial Intelligence (cs.AI), was
first submitted on 28 January 2022, and was last revised on 10 January 2023 as version 6. It carries
the arXiv-issued DOI 10.48550/arXiv.2201.11903 and is made available under a Creative Commons
Attribution 4.0 licence.

## Key Points

- The paper introduces chain-of-thought prompting: providing a few demonstrations of intermediate reasoning steps as exemplars in the prompt, which the authors describe as a simple method.
- Its central claim is that generating a chain of thought significantly improves large language models' ability to perform complex reasoning.
- The authors state that these reasoning abilities emerge naturally in sufficiently large language models, which ties the method's effect to model scale rather than to the prompting format alone.
- Experiments on three large language models are reported to improve performance across a range of arithmetic, commonsense and symbolic reasoning tasks.
- The headline result is that a 540B-parameter model prompted with eight chain-of-thought exemplars reaches state-of-the-art accuracy on GSM8K, a benchmark of math word problems, surpassing a finetuned GPT-3 with a verifier — a comparison between a prompting-only method and a trained baseline.

## Notes

The emergence claim is the paper's own qualifier on its result: the abstract attributes the reasoning
ability to models that are *sufficiently large*, so the reported gains are not presented as a property
of the prompting format on its own. The preprint went through six versions between January 2022 and
January 2023.
