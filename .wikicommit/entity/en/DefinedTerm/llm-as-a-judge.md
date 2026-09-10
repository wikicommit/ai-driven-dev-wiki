---
title: "LLM-as-a-Judge"
type: "schema:DefinedTerm"
lang: en
aliases: ["LLM-as-Judge"]
tags: [agents, llm, code-quality]
sources:
  - type: url
    url: https://github.com/NeoLabHQ/context-engineering-kit
    hash: sha256:3a00d5fa6029f48343ba32101feda4acd0f31870b7ff74ef954be99d4e04a584
    license: GPL-3.0
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "Having a separate model instance evaluate another's output against explicit rubrics and evidence, rather than accepting the output as produced — used in agent workflows as a quality gate between steps."
---

LLM-as-a-Judge is the practice of having a model evaluate output rather than produce it: a separate
instance scores or verifies work against structured rubrics, with the scoring expected to cite
evidence rather than assert a verdict. In agent workflows it is used as a gate between steps, where
a judge that withholds a pass sends the work back instead of letting it continue. The account below
is of how [[SoftwareApplication/context-engineering-kit]] applies the technique; that project treats
it as drawn from published research on evaluation patterns rather than as its own invention.

## Usage
The kit uses judging at two scales. As a quality gate it evaluates each planning and implementation
step of [[DefinedTerm/spec-driven-development]] against predefined verification rubrics before the
next step begins. As an execution primitive in
[[DefinedTerm/subagent-driven-development]] it appears in several forms: a judge run over finished
work with a structured rubric and evidence-based scoring; an independent judge paired with an
implementation sub-agent in a retry loop that repeats until the work passes; several judges in
iterative debate, which either build a consensus or report the disagreement rather than forcing one;
and a meta-judge sub-agent, used alongside judge sub-agents to generate specification material on
the fly. What the project asks of a judge in each case is
the same — a decision traceable to evidence and a rubric, not an opinion.

Independence is the property the arrangement depends on. The judge is described as separate from the
sub-agent that did the work, which is what makes the verdict worth more than the producing agent's
own confidence.

## When It Applies
It applies where the quality being checked can be written down as a rubric before the work is seen —
acceptance criteria, verification steps, review dimensions. Where the standard cannot be stated in
advance, there is nothing for a judge to score against, and the pattern degrades into asking a model
whether it likes the result.

The judge's own bias is treated as a first-class concern rather than an afterthought: the kit's
guidance on evaluating agent systems pairs LLM-as-a-Judge with multi-dimensional rubrics and bias
mitigation. Read the strongest claims made for it with that in mind — the
project states that judge-based quality gates fully eliminate cases where an agent produces
non-working or incorrect solutions, which is its own assessment of its own tooling, based on
internal production use rather than independent evaluation, and stronger than the surrounding
material supports.

## Related Terms
- [[DefinedTerm/subagent-driven-development]] — where judging is used as an execution primitive
- [[DefinedTerm/spec-driven-development]] — where it is used as a phase gate
