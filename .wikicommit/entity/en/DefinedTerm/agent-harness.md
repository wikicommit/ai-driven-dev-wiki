---
title: "agent harness"
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
  description: "The runtime orchestration layer that wraps an agent's core reasoning loop and coordinates tool execution, context management, safety enforcement, and session persistence around it — everything that happens after the first prompt, as distinct from the scaffolding that assembles the agent before it."
---

An agent harness is the runtime orchestration layer that wraps an agent's core reasoning loop and coordinates tool execution, context management, safety enforcement, and session persistence around it. [[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] defines it in explicit contrast to [[DefinedTerm/agent-scaffolding]]: where scaffolding is concerned with constructing the agent before the first prompt, the harness is concerned with everything that happens after — dispatching tools, compacting context, enforcing safety invariants, and persisting state across turns. The report credits the formalization of the term to Justin Young's writing on effective harnesses for long-running agents, describing it as the runtime framework that coordinates these concerns for agents operating over extended timeframes.

## Usage

In the architecture the report documents, the harness centres on a ReAct execution loop surrounded by supporting subsystems. Each iteration runs a fixed sequence of phases: draining any messages the UI thread injected since the last iteration, checking context pressure and applying reduction strategies, optionally producing a reasoning trace without tool access, calling the action model with the full tool schemas, dispatching any resulting tool calls through the registry, and deciding whether to iterate or return.

Seven subsystems sit around that loop, each addressing a distinct concern: a prompt composition engine that assembles the system prompt from modular, priority-ordered sections; a tool registry that dispatches to specialized handlers; a safety system providing defense in depth through multiple independent layers; a context engineering subsystem that treats the conversation as a finite resource; memory and session services that persist both the transcript and a playbook of learned strategies; and subagent orchestration that spawns isolated agent instances with filtered tool access.

The harness is also where several reliability mechanisms live that the reasoning model itself cannot provide. The report describes interrupt tokens polled at phase boundaries to propagate cancellation, a thread-safe injection queue so follow-up user messages are drained at iteration boundaries and checked before completion rather than being silently dropped, and cost tracking that records cumulative token usage after each model call. Termination is likewise a harness responsibility: the loop can end through explicit completion, implicit completion when the model returns text with no tool calls, exhaustion of an error-recovery budget, or an iteration safety cap — and before accepting termination the system checks for incomplete task items and pending messages.

The report presents the scaffolding/harness split itself as a transferable lesson, arguing that the separation prevents construction-time concerns from tangling with runtime concerns: the harness never checks whether the agent is fully initialized, because eager construction at scaffolding time guarantees it always is. The stated practical benefit is that each concern can evolve independently — adding a new tool requires only a registry change at construction time, while changing the compaction strategy requires only a harness change at runtime.

## Related Terms

The harness is one half of a pair with [[DefinedTerm/agent-scaffolding]]. Several of the mechanisms it coordinates have their own entries: [[DefinedTerm/adaptive-context-compaction]], [[DefinedTerm/system-reminders]], and [[DefinedTerm/subagents]]. The report positions the whole assembly as an instance of a compound AI system, in which state-of-the-art results come from composing multiple models, retrievers, and tools rather than relying on a single model call.
