---
title: "How we built our multi-agent research system"
type: "schema:TechArticle"
lang: en
tags: [multi-agent, evaluation, prompt-engineering, production-reliability]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/multi-agent-research-system'
    hash: sha256:f9af507dbe72a9650f1c11cf6ae2aa13e7f9c2f6c3a7436129197c31ddb3a3bc
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Anthropic's engineering account of taking a multi-agent Research feature from prototype to production, covering when multi-agent architectures pay for themselves, prompting principles for orchestration, evaluation of non-deterministic systems, and production reliability."
  author: ["Jeremy Hadfield", "Barry Zhang", "Kenneth Lien", "Florian Scholz", "Jeremy Fox", "Daniel Ford"]
  datePublished: "2025-06-13"
  publisher: "[[Organization/anthropic]]"
  proficiencyLevel: "Advanced"
---

This post describes the engineering behind Claude's Research feature, in which a lead agent plans a research process from a user query and then spawns parallel subagents that search simultaneously. Its stated framing is the distance between prototype and production: "the last mile often becomes most of the journey," because the compound nature of errors in agentic systems means minor issues that would be tolerable in traditional software can derail an agent entirely.

Its architecture is the orchestrator-worker pattern. A LeadResearcher agent thinks through its approach and saves the plan to memory to persist it — the post notes that a context window exceeding 200,000 tokens will be truncated, so retaining the plan matters — then creates specialised subagents with specific tasks. Each subagent searches independently, evaluates tool results with interleaved thinking, and returns findings. The lead synthesises and decides whether more research is needed. Once enough is gathered, findings pass to a CitationAgent that identifies specific locations for citations so claims are attributed to sources.

The post contrasts this with static retrieval-augmented generation, which fetches chunks most similar to the query; the multi-step search here dynamically finds relevant information, adapts to new findings, and analyses results.

## Key Practices

**Eight prompting principles** are given, drawn from failures the team observed — early agents spawned 50 subagents for simple queries, scoured the web endlessly for nonexistent sources, and distracted each other with excessive updates.

1. **Think like your agents.** The team built simulations in their Console with the system's exact prompts and tools and watched agents work step by step, which immediately revealed failure modes: continuing when results were already sufficient, using overly verbose queries, selecting incorrect tools.
2. **Teach the orchestrator how to delegate.** Each subagent needs an objective, an output format, guidance on tools and sources, and clear task boundaries. Vague instructions like "research the semiconductor shortage" led to subagents misinterpreting the task or repeating each other's searches — in one case, one subagent explored the 2021 automotive chip crisis while two others duplicated work on 2025 supply chains.
3. **Scale effort to query complexity.** Explicit rules were embedded in prompts: simple fact-finding gets one agent with 3-10 tool calls, direct comparisons 2-4 subagents with 10-15 calls each, complex research more than 10 subagents with clearly divided responsibilities.
4. **Tool design and selection are critical** — see [[DefinedTerm/agent-computer-interface]]. An agent searching the web for context that only exists in Slack "is doomed from the start," and MCP servers compound the problem by exposing unseen tools with descriptions of wildly varying quality.
5. **Let agents improve themselves.** Given a prompt and a failure mode, the models could diagnose why an agent was failing and suggest improvements.
6. **Start wide, then narrow down.** Agents default to overly long, specific queries returning few results; prompting them to start short and broad, evaluate what is available, then narrow, mirrors expert human research.
7. **Guide the thinking process.** Extended thinking serves as a controllable scratchpad — the lead agent uses it to plan, assess tool fit, determine query complexity and subagent count, and define each subagent's role; subagents use interleaved thinking after tool results to evaluate quality, identify gaps and refine the next query.
8. **Parallel tool calling transforms speed.** Two kinds of parallelism — the lead spinning up 3-5 subagents at once rather than serially, and subagents using three or more tools in parallel — cut research time by up to 90% for complex queries.

The stated strategy behind all eight is instilling good heuristics rather than rigid rules: the team studied how skilled humans research and encoded strategies such as decomposing difficult questions, evaluating source quality, adjusting approach on new information, and recognising when to go deep versus broad.

**Evaluation has to accommodate non-determinism.** Traditional evaluation assumes a fixed path from input to output, but agents may take completely different valid paths from identical starting points — one searching three sources, another ten. The post's answer is to judge whether agents achieved the right outcomes while following a reasonable process. Its practical advice is to start immediately with small samples, since early changes have dramatic effects (a prompt tweak moving success from 30% to 80%) that show up in a handful of cases; the team started with about 20 queries representing real usage. It argues against delaying evals until hundreds of test cases exist. [[DefinedTerm/llm-as-judge]] carried the scale, and human evaluation caught what automation missed — human testers noticed early agents consistently choosing SEO-optimised content farms over authoritative but lower-ranked sources like academic PDFs and personal blogs, which was fixed by adding source-quality heuristics to prompts.

**Production reliability needs different engineering.** Agents are stateful and errors compound, so restarts from the beginning are expensive and frustrating; the team built systems that resume from where the error occurred, and found that simply telling the agent a tool is failing and letting it adapt "works surprisingly well" — combined with deterministic safeguards like retry logic and regular checkpoints. Because agents are non-deterministic between runs even with identical prompts, full production tracing was added to diagnose failures, with monitoring of decision patterns and interaction structures rather than conversation contents, to maintain user privacy. Deployment uses rainbow deployments — gradually shifting traffic while keeping both versions running — because agents may be anywhere in their process when an update lands.

## Scope & Caveats

The post is explicit about cost and fit. Agents typically use about 4× more tokens than chat interactions, and multi-agent systems about 15× more, so "multi-agent systems require tasks where the value of the task is high enough to pay for the increased performance." Domains requiring all agents to share the same context, or with many dependencies between agents, are named as a poor fit today — with **coding called out specifically**, on the grounds that most coding tasks involve fewer truly parallelisable subtasks than research, and that LLM agents are not yet good at coordinating and delegating to each other in real time.

It also names a current architectural limit of its own system: lead agents execute subagents synchronously, waiting for each set to finish. That simplifies coordination but blocks the lead from steering subagents, prevents subagents from coordinating, and can stall the whole system on one slow subagent. Asynchronous execution is described as the next step, at the cost of harder result coordination, state consistency, and error propagation.

A final property the post emphasises is emergence: multi-agent systems exhibit behaviours that arise without specific programming, and small changes to the lead agent can unpredictably change subagent behaviour. Its conclusion from this is that the best prompts for such systems "are not just strict instructions, but frameworks for collaboration that define the division of labor, problem-solving approaches, and effort budgets."
