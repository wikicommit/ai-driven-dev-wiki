---
title: "Reflexion: Language Agents with Verbal Reinforcement Learning"
type: "schema:ScholarlyArticle"
lang: en
tags: [llm-agents, self-reflection, code-generation]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2303.11366'
    hash: sha256:d3cc06669bd2ade3e583039bd1298a3892c4c931b6ec1ee8f7a75064b1946261
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A 2023 arXiv paper proposing Reflexion, a framework that improves LLM-based agents through linguistic feedback instead of weight updates, by having agents reflect verbally on task feedback and store those reflections in an episodic memory for later trials."
  author: ["Noah Shinn", "Federico Cassano", "Edward Berman", "Ashwin Gopinath", "Karthik Narasimhan", "Shunyu Yao"]
  datePublished: "2023-03-20"
  keywords: ["Reflexion", "language agents", "verbal reinforcement learning", "episodic memory"]
---

This paper addresses a limitation of large language models used as goal-driven agents that interact with external environments such as games, compilers and APIs: learning quickly from trial and error is hard because traditional reinforcement learning needs many training samples and expensive fine-tuning. It proposes [[DefinedTerm/reflexion]], a framework that reinforces language agents through linguistic feedback rather than by updating model weights.

A Reflexion agent verbally reflects on task feedback signals and keeps the resulting reflective text in an episodic memory buffer, which it uses to make better decisions in subsequent trials. The authors evaluate it across sequential decision-making, coding and language-reasoning tasks and report significant improvements over a baseline agent.

## Key Points

- The framework reinforces agents through linguistic feedback, not weight updates or model fine-tuning.
- Agents reflect verbally on task feedback signals and maintain that reflective text in an episodic memory buffer to guide later trials.
- The framework accepts feedback signals of various types (scalar values or free-form language) and sources (external, or internally simulated).
- The authors report significant improvements over a baseline agent on sequential decision-making, coding and language-reasoning tasks.
- On the HumanEval coding benchmark, the paper reports 91% pass@1 accuracy, against 80% for GPT-4, which it describes as the previous state of the art.
- The paper includes ablation and analysis studies over different feedback signals, feedback-incorporation methods and agent types.

## Notes

The paper was first submitted to arXiv on 20 March 2023 and last revised on 10 October 2023 (version 4, which its comments say adds a few experiments). It is listed under Artificial Intelligence, Computation and Language, and Machine Learning.
