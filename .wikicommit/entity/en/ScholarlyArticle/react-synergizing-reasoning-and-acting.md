---
title: "ReAct: Synergizing Reasoning and Acting in Language Models"
type: "schema:ScholarlyArticle"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2210.03629'
    hash: sha256:ca951949ccc4fef896b47a6a7d3a59d0f707fcc7aa2e827e8fa8518efdb08728
  - type: url
    url: 'https://github.com/ysymyth/ReAct'
    hash: sha256:82875f618cf1b4628dd52d4ef96996f3226c75a80ae34f74b9a1a5367b7c1129
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A 2023 ICLR paper proposing ReAct, a method that prompts a large language model to interleave free-form reasoning ('thought') traces with task-specific actions in a single trajectory, and showing this combination outperforms reasoning-only and acting-only baselines on knowledge-intensive QA/fact-verification and on two interactive decision-making benchmarks."
  author: ["Shunyu Yao", "Jeffrey Zhao", "Dian Yu", "Nan Du", "Izhak Shafran", "Karthik Narasimhan", "Yuan Cao"]
  datePublished: "2023"
  keywords: ["ReAct", "large language models", "reasoning", "action", "agents"]
  citation: "Yao, Zhao, Yu, Du, Shafran, Narasimhan and Cao, \"ReAct: Synergizing Reasoning and Acting in Language Models\", International Conference on Learning Representations (ICLR), 2023."
---

This paper proposes [[DefinedTerm/react-prompting]], a method for prompting large language models to generate both free-form "thought" reasoning traces and task-specific actions in an interleaved trajectory, rather than studying reasoning (e.g. chain-of-thought) and acting (e.g. action-plan generation) as separate topics. A "thought" does not itself affect the external environment; instead, it composes useful information from the current context and updates the context to support later reasoning or acting, so the two are woven into a single stream the model reasons over. The authors prompt a frozen PaLM-540B model with one to six in-context examples per task, without any additional training.

The paper evaluates ReAct on knowledge-intensive reasoning tasks (HotpotQA multi-hop question answering and FEVER fact verification) where the model interacts with a simple Wikipedia API (`search[entity]`, `lookup[string]`, `finish[answer]`), and on two interactive decision-making benchmarks, ALFWorld (a text-based embodied household task) and WebShop (an online-shopping environment with real crawled product data).

## Key Points

- On HotpotQA and FEVER, combining ReAct's search-and-reason trajectories with self-consistency reasoning (CoT-SC → ReAct / ReAct → CoT-SC) outperformed either reasoning-only chain-of-thought or acting-only baselines used alone in the paper's PaLM-540B experiments.
- On ALFWorld, the paper reports the best of six ReAct trials reached a 71% overall success rate, compared with 45% for the best Act (action-only, no thoughts) trial and 37% for the BUTLER imitation-learning baseline; even ReAct's worst trial (48%) beat the best trial of either baseline.
- On WebShop, the paper reports ReAct achieved a score of 66.6 and a 40.0% success rate, versus 59.9/29.1% for an imitation-learning baseline and 62.4/28.7% for an imitation+reinforcement-learning baseline — an absolute 10-point success-rate improvement over the best prior method, matching the paper's abstract claim of a 10% absolute improvement on WebShop (and 34% on ALFWorld-type decision-making tasks, per the abstract).
- An ablation the paper calls ReAct-IM, using dense environment-feedback-style thoughts modeled on the prior Inner Monologue method, underperformed ordinary ReAct on ALFWorld (53% vs. 71% overall success rate), which the paper attributes to ReAct-IM more often failing to track subgoal completion and lacking commonsense reasoning about object locations.
- The paper positions ReAct against prior work: unlike Chain-of-Thought (Wei et al.) and its follow-ons, which the paper characterizes as reasoning performed in isolation from acting, ReAct integrates model actions and their observations into the reasoning stream; unlike WebGPT and chatbot/dialogue systems (BlenderBot, Sparrow, SimpleTOD), which the paper says do not explicitly model a reasoning procedure and rely on expensive human feedback or annotated datasets, ReAct's decision-making only requires language descriptions of the reasoning procedure. Separately, the paper credits Inner Monologue as the closest prior closed-loop system that ReAct builds on, while arguing Inner Monologue's "inner monologue" — limited to injected environment-state feedback — does not truly comprise inner thoughts the way ReAct's more flexible, sparse reasoning traces do.
- The paper's stated limitation is that complex tasks with large action spaces require more demonstrations to learn well, which can exceed the input-length limits of in-context learning; the authors report an initial fine-tuning experiment on HotpotQA as a promising direction to address this.

## Notes

The authors released the paper's GPT-3 prompting code as an MIT-licensed repository, with one
notebook per task for HotpotQA, FEVER, ALFWorld and WebShop, and a small Wikipedia environment for
the search-and-lookup interface. Running it requires an OpenAI API key and, for the household
simulation, a separate ALFWorld install. Because the two question-answering benchmarks have large
validation sets, the released notebooks evaluate on 500 randomly drawn development examples rather
than the full sets.

The paper itself already carries part of this comparison: an appendix sets PaLM-540B against GPT-3
(`text-davinci-002`) on two of the four tasks, reporting 29.4 against 30.8 exact match on HotpotQA
and 70.9% against 78.4% success on ALFWorld, and reads that as confirmation that ReAct prompting is
effective across different large language models. The repository extends the comparison to all
four, and on the two the appendix does not cover it puts GPT-3 behind: 54 against 62.2 exact match
on FEVER, and 35.8% against 40% success on WebShop. It summarises the whole picture as PaLM and
GPT-3 being better at different tasks.

Two of the repository's figures do not match the paper's. It gives GPT-3 at 30.4 exact match on
HotpotQA where the paper's appendix says 30.8, and lists 62.2 as the paper's own PaLM-540B result
on FEVER where the paper's tables and text report 60.9.
