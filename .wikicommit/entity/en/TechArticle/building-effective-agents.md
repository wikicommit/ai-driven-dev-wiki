---
title: "Building effective agents"
type: "schema:TechArticle"
lang: en
tags: [agent-architecture, workflow-patterns, tool-design]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/building-effective-agents'
    hash: sha256:89d6d2e67b90631137ed1aba80dbebb0264d98646e0db9850e22d6a6c80c67cf
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Anthropic's guidance on building LLM agents, arguing that the most successful implementations use simple composable patterns rather than complex frameworks, and cataloguing five workflow patterns plus the autonomous agent."
  author: ["Erik S.", "Barry Zhang"]
  datePublished: "2024-12-19"
  publisher: "[[Organization/anthropic]]"
  proficiencyLevel: "Intermediate"
---

This post distils what Anthropic learned working with dozens of teams building LLM agents across industries, and its headline finding is negative: "the most successful implementations weren't using complex frameworks or specialized libraries. Instead, they were building with simple, composable patterns."

Its organising distinction, described under [[DefinedTerm/agentic-system]], separates **workflows** — where LLMs and tools are orchestrated through predefined code paths — from **agents**, where LLMs dynamically direct their own processes and tool usage. The post catalogues five workflow patterns and one agent pattern, in increasing order of complexity, starting from the *augmented LLM*: a model enhanced with retrieval, tools and memory, which the post recommends tailoring to the use case and giving an easy, well-documented interface.

The page carries a note that much of the tooling landscape it describes has changed since December 2024, pointing readers to the [[TechArticle/scaling-managed-agents|Managed Agents]] work for the current approach.

## Key Practices

**Choose the least complex thing that works.** The recommendation is to find the simplest solution possible and increase complexity only when needed — which "might mean not building agentic systems at all," since agentic systems trade latency and cost for task performance. For many applications, optimising single LLM calls with retrieval and in-context examples is enough. Where more complexity is warranted, workflows offer predictability and consistency for well-defined tasks, while agents suit flexibility and model-driven decision-making at scale.

**Be wary of frameworks.** They simplify low-level tasks such as calling LLMs, defining and parsing tools, and chaining calls, but "often create extra layers of abstraction that can obscure the underlying prompts and responses, making them harder to debug," and make it tempting to add complexity where a simpler setup would do. The advice is to start with LLM APIs directly, since many patterns take a few lines of code, and if a framework is used, to understand the underlying code — incorrect assumptions about what is under the hood are named as a common source of customer error.

**The five workflow patterns.**

- **Prompt chaining** decomposes a task into a fixed sequence where each call processes the previous output, with optional programmatic gates on intermediate steps. It trades latency for accuracy by making each call an easier task, and fits tasks that decompose cleanly into fixed subtasks.
- **Routing** classifies an input and directs it to a specialised follow-up, allowing separation of concerns and more specialised prompts. It fits where there are distinct categories better handled separately and classification can be done accurately.
- **Parallelization** comes in two variations: *sectioning*, breaking a task into independent subtasks run in parallel, and *voting*, running the same task several times for diverse outputs. Its stated rationale is that for complex tasks with multiple considerations, models generally perform better when each consideration gets its own call.
- **Orchestrator-workers** has a central LLM dynamically break down tasks, delegate to workers, and synthesise the results. The post distinguishes it from parallelization explicitly: topographically similar, but the subtasks are not pre-defined — they are determined by the orchestrator from the specific input, which is why it fits work like multi-file code changes where you cannot predict the subtasks in advance.
- **Evaluator-optimizer** has one call generate a response while another evaluates it in a loop. Its two stated signs of good fit are that responses demonstrably improve when a human articulates feedback, and that the model can provide such feedback itself.

**Agents are simple loops with well-designed tools.** The post describes agents as "typically just LLMs using tools based on environmental feedback in a loop," beginning from a command or discussion with a human, then planning and operating independently while gaining ground truth from the environment at each step, pausing for human feedback at checkpoints or blockers. Because the implementation is straightforward, the leverage sits in toolset design and documentation — see [[DefinedTerm/agent-computer-interface]].

**Three core principles** close the post: maintain simplicity in the agent's design; prioritise transparency by explicitly showing the agent's planning steps; and carefully craft the agent-computer interface through thorough tool documentation and testing.

## Scope & Caveats

The post states the cost of autonomy plainly: agents mean higher costs and the potential for compounding errors, so it recommends extensive testing in sandboxed environments with appropriate guardrails, and stopping conditions such as a maximum iteration count to maintain control. Agents suit open-ended problems where the number of steps cannot be predicted and a fixed path cannot be hardcoded — and require "some level of trust" in the model's decision-making, which is why the post frames their autonomy as ideal for scaling tasks *in trusted environments*.

Its appendix on where agents pay off names two domains — customer support and coding — and identifies what they share: tasks requiring both conversation and action, clear success criteria, feedback loops, and meaningful human oversight. For coding specifically it notes that solutions are verifiable through automated tests and that quality can be measured objectively, while adding that "human review remains crucial for ensuring solutions align with broader system requirements."

The patterns are explicitly not prescriptive: they are "common patterns that developers can shape and combine," with the stated key to success being measurement and iteration, and complexity added only when it demonstrably improves outcomes.
