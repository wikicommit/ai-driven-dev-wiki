---
title: "ReAct"
type: "schema:DefinedTerm"
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
  description: "A prompting technique, proposed by Yao et al., that augments a language model agent's action space with a 'language space' of free-form thoughts, so the model interleaves reasoning traces with task-specific actions in a single trajectory instead of treating reasoning and acting as separate capabilities."
---

ReAct is a prompting technique, proposed by Yao et al. in [[ScholarlyArticle/react-synergizing-reasoning-and-acting]], that augments an agent's action space with a "language space" of free-form thoughts alongside its ordinary task-specific actions. A thought does not itself act on the external environment and produces no observation feedback; instead, it composes useful information from the current context — such as decomposing a goal, tracking progress, or noting an exception — and updates the context to support later reasoning or acting. The technique is applied by prompting a frozen large language model with a handful of in-context examples, each a human-written trajectory of thoughts, actions, and environment observations, without any additional model training.

## When It Applies

The introducing paper applies ReAct to tasks with distinct action spaces and reasoning needs: for knowledge-intensive tasks (multi-hop question answering, fact verification) it alternates thought and action steps densely, interacting with a simple Wikipedia search/lookup interface to retrieve supporting information; for interactive decision-making tasks (a text-based household simulation and an online-shopping environment) it lets thoughts appear more sparsely, at the points in a trajectory where they are most useful, with the language model itself deciding when to think versus act. The paper reports that ReAct outperformed both reasoning-only and acting-only baselines across these settings, and that an ablation using dense, externally-triggered thoughts modeled on a prior "Inner Monologue" method underperformed ReAct's sparser, more flexible thought pattern on the household-simulation task. The paper's own stated limitation is that tasks with large action spaces need more demonstrations to learn well, which can exceed the input-length limits of in-context prompting.

## Related Terms

[[ScholarlyArticle/react-synergizing-reasoning-and-acting]]
