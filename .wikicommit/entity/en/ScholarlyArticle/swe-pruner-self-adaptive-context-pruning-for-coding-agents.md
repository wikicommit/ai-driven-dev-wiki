---
title: "SWE-Pruner: Self-Adaptive Context Pruning for Coding Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, context-management, token-efficiency]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2601.16746'
    hash: sha256:b0deab8dd25599561bb8c1c203b55a00bc43553266e9baf83107047eb79079d6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An arXiv paper proposing SWE-Pruner, a self-adaptive context pruning framework for coding agents in which the agent states an explicit goal and a lightweight neural skimmer selects the context lines relevant to it."
  author: ["Yuhang Wang", "Yuling Shi", "Mo Yang", "Rongrui Zhang", "Shilin He", "Heng Lian", "Yuting Chen", "Siyu Ye", "Kai Cai", "Xiaodong Gu"]
  datePublished: "2026-01-23"
  keywords: ["coding agents", "context pruning", "context compression", "token reduction"]
---

The paper starts from the observation that LLM agents perform well in software development but are held back by long interaction contexts, which incur high API costs and latency. It argues that existing context compression approaches, such as LongLLMLingua, typically rely on fixed metrics such as perplexity and ignore the task-specific nature of code understanding, so they frequently disrupt syntactic and logical structure and fail to retain critical implementation details.

In response it proposes SWE-Pruner, a self-adaptive context pruning framework tailored for coding agents. Drawing on how human programmers "selectively skim" source code while developing and debugging, SWE-Pruner performs task-aware adaptive pruning: given the current task, the agent formulates an explicit goal (the paper's example is "focus on error handling") as a hint that guides what is pruned, and a lightweight neural skimmer of 0.6B parameters is trained to dynamically select the relevant lines from the surrounding context given that goal.

## Key Points

- Existing context compression methods that rely on fixed metrics such as perplexity, the authors argue, frequently break the syntactic and logical structure of code and drop critical implementation details.
- SWE-Pruner has the coding agent state an explicit goal for the current task, which is used as a hint to guide which context is pruned.
- A trained neural skimmer with 0.6B parameters selects the lines relevant to that goal from the surrounding context.
- Evaluated across four benchmarks and multiple models, SWE-Pruner achieves 23-54% token reduction on agent tasks such as [[Dataset/swe-bench-verified]] while even improving success rates, according to the paper.
- On single-turn tasks such as LongCodeQA it reaches up to 14.84x compression with minimal performance impact, according to the paper.

## Notes

The paper was first submitted to arXiv on 23 January 2026 and last revised on 7 May 2026 (version 4). It is filed under Software Engineering (cs.SE) and Computation and Language (cs.CL), and the authors state that its code is publicly available.
