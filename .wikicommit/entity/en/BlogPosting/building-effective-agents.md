---
title: "Building effective agents"
type: "schema:BlogPosting"
lang: en
tags: [agent-architecture, tool-use, agents]
sources:
  - type: url
    url: 'https://www.anthropic.com/research/building-effective-agents'
    hash: sha256:611504eb30423330be060ed8f00e432a0adcb417f992b2cfb5cbf9ccd8d511bf
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Anthropic's account of what worked across dozens of customer teams building LLM agents: simple composable patterns rather than frameworks. It draws the workflows-versus-agents distinction, sets out five named workflow patterns and the autonomous agent, and argues for adding complexity only when it demonstrably improves outcomes."
  author: ["Erik S.", "Barry Zhang"]
  datePublished: "2024-12-19"
  publisher: "[[Organization/anthropic]]"
---

This post reports what Anthropic observed across dozens of teams building LLM agents, and its headline
finding is negative: the most successful implementations were not using complex frameworks or
specialized libraries, but simple, composable patterns. Most of the post is an inventory of those
patterns, arranged by increasing complexity from a single augmented model call up to an autonomous
agent, with a statement for each of when it is the right choice.

Its central vocabulary move is a distinction it declines to resolve by argument. Anthropic groups everything under the heading
**agentic systems** and then separates two kinds: **workflows**, where LLMs and tools are orchestrated
through predefined code paths, and **agents**, where the LLM dynamically directs its own process and
tool usage, keeping control of how it accomplishes the task. The practical weight of the distinction is
in the recommendation attached to it — workflows give predictability and consistency for well-defined
tasks, agents are the better choice where flexibility and model-driven decision-making are needed at
scale, and for many applications optimizing single LLM calls with retrieval and in-context examples is
enough.

The post carries a note that much of the tooling landscape it describes has changed since December
2024, pointing readers to Anthropic's more recent writing on managed agents for its current approach.

## Key Points

- The stated general rule is to find the simplest solution possible and increase complexity only when
  needed — which the post says may mean not building an agentic system at all, since agentic systems
  trade latency and cost for task performance.
- On frameworks, the recommendation is to start with LLM APIs directly, on the grounds that many patterns
  take a few lines of code; frameworks are said to simplify low-level tasks but to add abstraction layers
  that obscure prompts and responses, make debugging harder, and invite complexity a simpler setup would
  not need. Incorrect assumptions about what a framework does underneath are named as a common source of
  customer error.
- The foundational building block is the [[DefinedTerm/augmented-llm]] — a model enhanced with
  retrieval, tools and memory, generating its own search queries, selecting tools and deciding what to
  retain. The post recommends tailoring these capabilities to the use case and giving the model an easy,
  well-documented interface, and names [[DefinedTerm/model-context-protocol]] as one way to implement
  them.
- **Prompt chaining** decomposes a task into a fixed sequence where each call processes the previous
  output, with optional programmatic gates between steps; its stated purpose is trading latency for
  accuracy by making each call easier, and it suits tasks that decompose cleanly into fixed subtasks.
- **Routing** classifies an input and directs it to a specialized follow-up, allowing separation of
  concerns and more specialized prompts; the post notes that without it, optimizing for one kind of input
  can hurt performance on others. Its examples include directing support query types to different
  downstream processes, and sending easy questions to smaller models and hard ones to more capable ones.
- **Parallelization** comes in two variations: *sectioning*, breaking a task into independent subtasks
  run in parallel, and *voting*, running the same task several times for diverse outputs. The post states
  that for complex tasks with multiple considerations, LLMs generally perform better when each
  consideration gets its own call.
- One sectioning example is a guardrail arrangement where one model instance handles the user query while
  another screens it for inappropriate content — which the post says tends to perform better than having
  one call do both.
- **Orchestrator-workers** has a central LLM dynamically break down a task, delegate to worker LLMs and
  synthesize the results. The post distinguishes it from parallelization by flexibility rather than
  topology: the subtasks are not predefined but determined by the orchestrator from the input. Its named
  examples are coding products making complex changes across multiple files, and multi-source search.
- **Evaluator-optimizer** puts one call to generating a response and another to evaluating it in a loop.
  Its examples are literary translation, where an evaluator can supply critiques the translator missed,
  and complex search where the evaluator decides whether further searching is warranted.
- Agents are described as beginning from a human command or discussion, then planning and operating
  independently, with the post stressing that they must gain "ground truth" from the environment at each
  step — tool call results, code execution — to assess progress, and can pause for human feedback at
  checkpoints or blockers.
- Implementation is characterised as straightforward even where the tasks are sophisticated: agents are
  "typically just LLMs using tools based on environmental feedback in a loop", which the post gives as
  the reason toolsets and their documentation must be designed carefully.
- Including stopping conditions such as a maximum number of iterations is described as common practice
  for maintaining control, and the
  post names higher cost and compounding errors as the price of autonomy, recommending extensive testing
  in sandboxed environments with appropriate [[DefinedTerm/guardrails]].
- Agents are said to suit open-ended problems where the number of steps cannot be predicted and no fixed
  path can be hardcoded, and to require some level of trust in the model's decision-making — which the
  post ties to deploying them in trusted environments.
- Three closing principles are stated for implementing agents: maintain simplicity in the design,
  prioritize transparency by explicitly showing the planning steps, and carefully craft the
  agent-computer interface through thorough tool documentation and testing.
- The patterns are explicitly offered as non-prescriptive building blocks to be combined, with the
  repeated instruction to add complexity only when it demonstrably improves outcomes.

## Context

The evidence base is Anthropic's own consulting experience — work with dozens of customer teams plus its
own agent building — reported qualitatively. No measurements accompany any pattern, and the post makes no
claim that its inventory is complete; the two agent examples it offers as its own are a coding agent for
SWE-bench tasks and a computer use reference implementation.

The post is careful that "agent" is defined in several ways by others, which is the reason it
introduces the umbrella term "agentic systems" rather than arguing for one definition — and why the
line it does draw is architectural (who directs the process) rather than a claim about which usage is
correct.

The post's own dating note matters for how to read it: Anthropic states that much of the tooling
landscape described has changed since December 2024 and points to its later writing for its current
approach, so the pattern inventory should be read as durable while the specific framework and product
references should not.
