---
title: "Chain-of-Thought Prompting"
type: "schema:DefinedTerm"
lang: en
aliases: ["Chain of Thought"]
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
  description: "A prompting method, proposed by Wei et al., in which a few demonstrations showing intermediate reasoning steps are supplied as exemplars so the model generates its own series of intermediate steps before answering."
---

Chain-of-thought prompting is a method, proposed by Wei et al. in
[[ScholarlyArticle/chain-of-thought-prompting-elicits-reasoning-in-large-language-models]], in which
a few chain-of-thought demonstrations are provided as exemplars in the prompt. A chain of thought is
a series of intermediate reasoning steps, and generating one is what the authors report
significantly improves a large language model's ability to perform complex reasoning. The authors
describe it as a simple method, and what it consists of is the exemplars themselves: a handful of
worked demonstrations placed in the prompt.

## Usage

The paper reports the method applied across arithmetic, commonsense and symbolic reasoning tasks,
evaluated on three large language models, with improvements on all three task families. Its headline
demonstration is small in prompt terms and large in effect: a 540B-parameter model given eight
chain-of-thought exemplars reached state-of-the-art accuracy on GSM8K, a benchmark of math word
problems, surpassing a finetuned GPT-3 with a verifier — that is, a prompting-only method
outperforming a trained baseline on that benchmark.

## When It Applies

The condition the authors attach to the method is model scale: they state that the reasoning
abilities it elicits emerge naturally in *sufficiently large* language models, so the format alone is
not presented as sufficient. It assumes a few-shot prompting setting in which exemplars can be
placed in the prompt, and it assumes those exemplars can be written to display the intermediate
steps the task actually requires. The evidence behind it is the paper's own: experiments on three
large language models over arithmetic, commonsense and symbolic reasoning tasks, reported in a
preprint first submitted in January 2022 and last revised in January 2023.

## Related Terms

[[DefinedTerm/react-prompting]], [[DefinedTerm/prompt-engineering]],
[[DefinedTerm/plan-act-observe-loop]]
