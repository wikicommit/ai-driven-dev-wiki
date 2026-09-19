---
title: "ReAct"
type: "schema:DefinedTerm"
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
  description: "A prompting technique, proposed by Yao et al., that augments a language model agent's action space with a 'language space' of free-form thoughts, so the model interleaves reasoning traces with task-specific actions in a single trajectory instead of treating reasoning and acting as separate capabilities."
---

ReAct is a prompting technique, proposed by Yao et al. in [[ScholarlyArticle/react-synergizing-reasoning-and-acting]], that augments an agent's action space with a "language space" of free-form thoughts alongside its ordinary task-specific actions. A thought does not itself act on the external environment and produces no observation feedback; instead, it composes useful information from the current context — such as decomposing a goal, tracking progress, or noting an exception — and updates the context to support later reasoning or acting. The technique is applied by prompting a frozen large language model with a handful of in-context examples, each a human-written trajectory of thoughts, actions, and environment observations, without any additional model training.

## Usage

The technique is applied by writing the in-context examples by hand, one set per task, and the
authors published theirs as an MIT-licensed repository of GPT-3 prompting code — a notebook per
task, with a small Wikipedia environment supplying the search-and-lookup actions. That repository
directs readers who want to apply ReAct to tasks beyond the four it covers to
[[SoftwareApplication/langchain]]'s zero-shot ReAct agent rather than to its own prompts.

How far the technique carries across models is read differently by the two documents. The paper's
appendix compares PaLM-540B with GPT-3 (`text-davinci-002`) on two tasks, finds GPT-3 ahead on
both, and reads that as evidence that ReAct prompting is effective across different large language
models. The repository's table covers four tasks and has GPT-3 ahead on two and behind on the other
two, which it summarises as the two models being better at different tasks.

## When It Applies

The introducing paper applies ReAct to tasks with distinct action spaces and reasoning needs: for knowledge-intensive tasks (multi-hop question answering, fact verification) it alternates thought and action steps densely, interacting with a simple Wikipedia search/lookup interface to retrieve supporting information; for interactive decision-making tasks (a text-based household simulation and an online-shopping environment) it lets thoughts appear more sparsely, at the points in a trajectory where they are most useful, with the language model itself deciding when to think versus act. The paper reports that ReAct consistently outperformed the acting-only baseline; against reasoning-only chain-of-thought it came out ahead on fact verification but slightly behind on multi-hop question answering, and the paper's strongest results on those two tasks came from combining ReAct with self-consistency reasoning rather than from ReAct alone. It also reports that an ablation using dense, externally-triggered thoughts modeled on a prior "Inner Monologue" method underperformed ReAct's sparser, more flexible thought pattern on the household-simulation task. The paper's own stated limitation is that tasks with large action spaces need more demonstrations to learn well, which can exceed the input-length limits of in-context prompting.

## Related Terms

[[ScholarlyArticle/react-synergizing-reasoning-and-acting]]
