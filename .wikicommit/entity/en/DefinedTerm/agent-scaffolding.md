---
title: "agent scaffolding"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05344'
    hash: sha256:29a5dfd46c7505affc599f6922ebba2f67d01e7f3a343df5347a42f435a08edc
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The construction phase that assembles an agent before its first prompt — compiling the system prompt, building tool schemas, and registering subagents — as distinct from the harness that orchestrates the agent's behavior at runtime."
---

Agent scaffolding is the construction phase that assembles an agent before the first prompt arrives. [[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] uses the term for the step in which the system prompt is compiled, tool schemas are built, and subagents are registered, and pairs it with the [[DefinedTerm/agent-harness]], which handles everything that happens after construction at runtime.

## Usage

The report describes an *eager construction* design in which an agent's constructor builds both the system prompt and the tool schemas before returning, so that by the time construction completes the agent is fully ready to serve requests, with no lazy prompt assembly and no first-call latency. It contrasts this with an earlier lazy approach that built the system prompt on the first run: that introduced first-call latency visible to the user and caused race conditions with tool discovery, because tools registered after the first call would not appear in the prompt until a manual refresh.

Two further design pivots are recorded. An early class hierarchy with separate classes for planning agents, code-exploration agents, and web-generation agents was replaced by a single parameterized agent class, because the hierarchy created a diamond problem when subagents needed mixed capabilities — such as a web generator that also plans. Behavioral variation instead comes entirely from construction parameters: an allowlist that filters which tool schemas appear in the agent's schema, a system prompt override, and a flag derived from whether the allowlist is non-null. Separately, inline subagent definitions hardcoded within the main agent's code were replaced by a registration system, so that custom agents defined in configuration files go through the same compilation path as built-in ones.

Assembly is centralized in a factory that executes three phases in strict order: discovering and registering skill definitions, compiling and registering subagent specifications, and finally constructing the main agent with no tool filtering. The report notes the ordering constraint is essential — subagents must be registered before the main agent is constructed, because the subagent-spawning tool's description is dynamically built from the set of registered agents and must be present in the main agent's schema.

Scaffolding is also where one of the report's safety arguments takes effect. Because a subagent's tool schema is filtered at build time, tools outside its allowlist are never visible to it; the report describes this as making violations structurally impossible rather than blocked, on the grounds that a model cannot reason about capabilities it does not know exist.

## Related Terms

Scaffolding is one half of a pair with the [[DefinedTerm/agent-harness]]. The filtered agents it compiles are [[DefinedTerm/subagents]], and the modular system prompt it assembles is one of the artifacts managed under [[DefinedTerm/context-engineering]].
