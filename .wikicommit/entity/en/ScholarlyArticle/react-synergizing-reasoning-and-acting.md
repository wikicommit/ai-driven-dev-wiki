---
title: "ReAct: Synergizing Reasoning and Acting in Language Models"
type: "schema:ScholarlyArticle"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2210.03629'
    hash: sha256:ca951949ccc4fef896b47a6a7d3a59d0f707fcc7aa2e827e8fa8518efdb08728
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A 2023 ICLR paper proposing ReAct, a method that prompts a large language model to interleave free-form reasoning ('thought') traces with task-specific actions in a single trajectory, and showing this combination outperforms reasoning-only and acting-only baselines on knowledge-intensive QA/fact-verification and on two interactive decision-making benchmarks."
  author: ["Shunyu Yao", "Jeffrey Zhao", "Dian Yu", "Nan Du", "Izhak Shafran", "Karthik Narasimhan", "Yuan Cao"]
  keywords: ["ReAct", "large language models", "reasoning", "action", "agents"]
---

This paper proposes [[DefinedTerm/react-prompting]], a method for prompting large language models to generate both free-form "thought" reasoning traces and task-specific actions in an interleaved trajectory, rather than studying reasoning (e.g. chain-of-thought) and acting (e.g. action-plan generation) as separate topics. A "thought" does not itself affect the external environment; instead, it composes useful information from the current context and updates the context to support later reasoning or acting, so the two are woven into a single stream the model reasons over. The authors prompt a frozen PaLM-540B model with one to six in-context examples per task, without any additional training.

The paper evaluates ReAct on knowledge-intensive reasoning tasks (HotpotQA multi-hop question answering and FEVER fact verification) where the model interacts with a simple Wikipedia API (`search[entity]`, `lookup[string]`, `finish[answer]`), and on two interactive decision-making benchmarks, ALFWorld (a text-based embodied household task) and WebShop (an online-shopping environment with real crawled product data).

## Key Points

- On HotpotQA and FEVER, combining ReAct's search-and-reason trajectories with self-consistency reasoning (CoT-SC → ReAct / ReAct → CoT-SC) outperformed either reasoning-only chain-of-thought or acting-only baselines used alone in the paper's PaLM-540B experiments.
- On ALFWorld, the paper reports ReAct's best trial reached a 71% average success rate across six controlled trials, compared with 45% for the best Act (action-only, no thoughts) trial and 37% for the BUTLER imitation-learning baseline; even ReAct's worst trial (48%) beat the best trial of either baseline.
- On WebShop, the paper reports ReAct achieved a score of 66.6 and a 40.0% success rate, versus 59.9/29.1% for an imitation-learning baseline and 62.4/28.7% for an imitation+reinforcement-learning baseline — an absolute 10-point success-rate improvement over the best prior method, matching the paper's abstract claim of a 10% absolute improvement on WebShop (and 34% on ALFWorld-type decision-making tasks, per the abstract).
- An ablation the paper calls ReAct-IM, using dense environment-feedback-style thoughts modeled on the prior Inner Monologue method, underperformed ordinary ReAct on ALFWorld (53% vs. 71% overall success rate), which the paper attributes to ReAct-IM more often failing to track subgoal completion and lacking commonsense reasoning about object locations.
- The paper positions ReAct against prior work: unlike Chain-of-Thought (Wei et al.) and its follow-ons, which the paper characterizes as reasoning performed in isolation from acting, ReAct integrates model actions and their observations into the reasoning stream; unlike WebGPT and chatbot/dialogue systems (BlenderBot, Sparrow, SimpleTOD), which the paper says do not explicitly model a reasoning procedure and rely on expensive human feedback or annotated datasets, ReAct's decision-making only requires language descriptions of the reasoning procedure. Separately, the paper credits Inner Monologue as the closest prior closed-loop system that ReAct builds on, while arguing Inner Monologue's "inner monologue" — limited to injected environment-state feedback — does not truly comprise inner thoughts the way ReAct's more flexible, sparse reasoning traces do.
- The paper's stated limitation is that complex tasks with large action spaces require more demonstrations to learn well, which can exceed the input-length limits of in-context learning; the authors report an initial fine-tuning experiment on HotpotQA as a promising direction to address this.

## Notes

This entry is based on the paper's main text (introduction, methods, results, related work, and conclusion sections); the OCR/text-extraction of several figures and tables in the source is visually garbled, so numeric results are drawn from the surrounding prose and from readable table cells rather than from the garbled table layouts themselves.
