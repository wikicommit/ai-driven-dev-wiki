---
title: "Reflexion"
type: "schema:DefinedTerm"
lang: en
tags: [llm-agents, self-reflection]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2303.11366'
    hash: sha256:d3cc06669bd2ade3e583039bd1298a3892c4c931b6ec1ee8f7a75064b1946261
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A framework, proposed by Shinn et al. in 2023, that reinforces LLM-based agents through linguistic feedback instead of weight updates: the agent reflects verbally on task feedback and keeps those reflections in an episodic memory to improve decisions in later trials."
---

Reflexion is a framework for improving language agents — large language models acting as goal-driven agents in environments such as games, compilers and APIs — through linguistic feedback rather than by updating model weights, proposed in [[ScholarlyArticle/reflexion-language-agents-with-verbal-reinforcement-learning]]. After an attempt at a task, a Reflexion agent reflects verbally on the feedback signal it received and stores that reflective text in an episodic memory buffer; in subsequent trials the stored reflections are used to induce better decision-making. The feedback can be a scalar value or free-form language, and can come from an external source or be simulated internally.

## Usage

Its authors present it as an alternative to traditional reinforcement learning for language agents, which they describe as needing extensive training samples and expensive fine-tuning. They apply it to sequential decision-making, coding and language-reasoning tasks; on the HumanEval coding benchmark they report 91% pass@1, against 80% for GPT-4.

## When It Applies

It applies where an agent makes repeated attempts at a task and receives some feedback signal about each attempt that can be turned into a verbal reflection. It assumes the agent can carry that reflective text forward into later trials through its memory, rather than learning through model training. The evidence for it at the level recorded here is the proposing paper's own evaluation, which reports improvements over a baseline agent and includes ablations over feedback signals, feedback-incorporation methods and agent types.

## Related Terms

- [[DefinedTerm/react-prompting]]
- [[DefinedTerm/verification-loop]]
