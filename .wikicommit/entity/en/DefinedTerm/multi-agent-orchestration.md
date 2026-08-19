---
title: "multi-agent orchestration"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, context-engineering, agentic-coding]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://www.langchain.com/blog/context-engineering-for-agents'
    hash: sha256:07e9475327ca11aeabb710cea3b419188e2ca4380d3cf4fd055291761f52fb8f
  - type: url
    url: 'https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf'
    hash: sha256:c63d41952636629543bbc11004c9be52b96f346284383c32bcd91f9130d25932
  - type: url
    url: 'https://ghuntley.com/ralph/'
    hash: sha256:9836ee3ee0773613f370a27796b1e456199be38681f73a47b974e210dd356317
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Splitting work across several agents that each hold their own context window, with a lead agent coordinating them — used both to isolate context so no single window fills up and to explore several parts of a problem in parallel."
  termCode: ""
  inDefinedTermSet: ""
---

Multi-agent orchestration is the practice of splitting work across several agents that each hold their own context window, coordinated by a lead agent or orchestrator. Its two stated motivations are context isolation — no single window accumulates everything — and parallelism, since separate agents can explore different parts of a problem simultaneously. It is one of the standard answers to the context window being a finite resource, alongside [[DefinedTerm/compaction]] and [[DefinedTerm/agentic-memory]].

## Usage

[[TechArticle/effective-context-engineering-for-ai-agents]] describes the architecture concretely: rather than one agent maintaining state across an entire project, specialised sub-agents handle focused tasks with clean context windows while the main agent coordinates with a high-level plan. Each sub-agent might explore extensively, using tens of thousands of tokens or more, but returns only a condensed summary — the post gives a figure of roughly 1,000–2,000 tokens. Its stated benefit is a clear separation of concerns, with detailed search context isolated inside sub-agents while the lead agent synthesises and analyses results. That post also matches the approach to a task shape, recommending it for complex research and analysis where parallel exploration pays dividends, over compaction for conversational back-and-forth and note-taking for iterative development with clear milestones.

[[BlogPosting/context-engineering]] treats the same architecture as the most popular way to *isolate* context in its four-bucket taxonomy, noting that each agent has its own tools, instructions, and context window, and citing separation of concerns as the motivation behind OpenAI's Swarm library. It also states the costs plainly: up to 15× more tokens than chat as reported by Anthropic, the need for careful prompt engineering to plan sub-agent work, and coordination overhead.

[[Report/2026-agentic-coding-trends-report]] treats the shift from single agents to coordinated teams as one of its eight predicted 2026 trends, and describes what adopting it demands: new skills in task decomposition, agent specialisation, and coordination protocols, along with development environments that show the status of multiple concurrent agent sessions and version control workflows that handle simultaneous agent-generated contributions. Its customer example is Fountain's hierarchical orchestration, with a central orchestration agent coordinating specialised sub-agents for candidate screening, document generation, and sentiment analysis.

Not every practitioner reaches for it. [[Person/geoffrey-huntley]] argues in [[BlogPosting/ralph-wiggum-as-a-software-engineer]] that agent-to-agent communication and multiplexing were not needed at the time, comparing non-deterministic agents-as-microservices unfavourably to a single monolithic process — while still using [[DefinedTerm/subagents]] heavily within that single process, dispatched by the primary context window acting as a scheduler.

## Related Terms

The mechanism it is built from is covered under [[DefinedTerm/subagents]], and one specific discipline for applying it under [[DefinedTerm/subagent-driven-development]]. It is one of the strategies of [[DefinedTerm/context-engineering]], and the evaluation step it usually pairs with is [[DefinedTerm/llm-as-judge]]. Frameworks providing building blocks for it include [[SoftwareApplication/langgraph]] and [[SoftwareApplication/context-engineering-kit]].
