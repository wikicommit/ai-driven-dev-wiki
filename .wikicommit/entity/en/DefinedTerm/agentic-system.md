---
title: "agentic system"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, terminology, workflow-patterns]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/building-effective-agents'
    hash: sha256:89d6d2e67b90631137ed1aba80dbebb0264d98646e0db9850e22d6a6c80c67cf
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Anthropic's umbrella term for systems built around LLMs and tools, subdividing into workflows — orchestrated through predefined code paths — and agents, which dynamically direct their own processes and tool usage."
  termCode: ""
  inDefinedTermSet: ""
---

*Agentic system* is the umbrella term [[TechArticle/building-effective-agents]] uses to cover the range of things people call agents, and its purpose is to make room for an architectural distinction inside it. That post notes that some define agents as fully autonomous systems operating independently over extended periods, while others use the term for more prescriptive implementations following predefined workflows — and categorises both as agentic systems while separating:

- **Workflows** — systems where LLMs and tools are orchestrated through *predefined code paths*.
- **Agents** — systems where LLMs *dynamically direct their own processes and tool usage*, maintaining control over how they accomplish tasks.

The distinction is architectural rather than about capability or autonomy level: what differs is who decides the sequence.

## Usage

**The building block underneath both** is the *augmented LLM*: a model enhanced with retrieval, tools and memory, able to generate its own search queries, select appropriate tools, and determine what information to retain. That post's recommendation for it is twofold — tailor the augmentations to the specific use case, and give the model an easy, well-documented interface, with [[DefinedTerm/model-context-protocol]] named as one way to implement them.

**Five workflow patterns** are catalogued in increasing complexity. *Prompt chaining* runs a fixed sequence where each call processes the previous output, with optional programmatic gates. *Routing* classifies an input and directs it to a specialised follow-up. *Parallelization* splits into sectioning (independent subtasks at once) and voting (the same task run several times for diverse outputs). *Orchestrator-workers* has a central model decompose the task at runtime, delegate, and synthesise. *Evaluator-optimizer* pairs a generator with a critic in a loop.

**The agent pattern** is the one where the path is not predetermined at all: an agent begins from a command or discussion with a human, then plans and operates independently, gaining ground truth from the environment at each step and pausing for feedback at checkpoints or blockers. That post describes the implementation as usually straightforward — "typically just LLMs using tools based on environmental feedback in a loop" — which is why it locates the difficulty in the [[DefinedTerm/agent-computer-interface]] rather than the loop.

**The selection rule** is to prefer the simplest thing that works, on the grounds that agentic systems trade latency and cost for task performance. Workflows are recommended where predictability and consistency matter for well-defined tasks; agents where flexibility and model-driven decision-making are needed at scale; and for many applications, neither — just a single LLM call optimised with retrieval and in-context examples.

## Related Terms

The orchestrator-workers pattern is the workflow form of [[DefinedTerm/multi-agent-orchestration]], and the evaluator-optimizer pattern is [[DefinedTerm/llm-as-judge]] arranged as a loop rather than a gate. A [[DefinedTerm/coding-agent]] is the agent end of this spectrum applied to software, and the loop it runs is wrapped by an [[DefinedTerm/agent-harness]].
