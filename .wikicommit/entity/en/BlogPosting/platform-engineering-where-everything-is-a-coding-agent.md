---
title: "2026 年，万物皆 Coding Agent 的平台工程（A2A / ACP / MCP / Skill）"
type: "schema:BlogPosting"
lang: en
tags: [platform-engineering, agent-protocols, multi-agent, coding-agents, mcp]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/coding-agent-platform-engineering/'
    hash: sha256:8dfe0d1a99160baa5c9e267af55b3724ec49f6cd505455926157bf819fb2a673
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A March 2026 Chinese-language blog post by Phodal Huang on the trend he expects for the year: platform engineering built from many coding agents, connected by the MCP, ACP and A2A protocols plus Skills, and coordinated by an orchestration layer. It contrasts external orchestration with a Workspace Agent mode and uses the Routa platform as a reference implementation."
  author: ["Phodal Huang"]
  datePublished: "2026-03-03"
---

This post, written in Chinese by Phodal Huang as his take on the year's trend, starts from the
observation that each part of the DevOps toolchain — CI/CD, issues, testing, documentation, pull
requests, the IDE — is growing its own AI agent. He argues that no single agent covers the whole flow,
so the agents end up as isolated islands, and that the question for platform engineering becomes who
orchestrates them. His answer is to standardise the capabilities scattered through the toolchain with
[[DefinedTerm/agent2agent-protocol]] (A2A), the [[DefinedTerm/agent-client-protocol]] (ACP),
[[DefinedTerm/model-context-protocol]] (MCP) and Skills, so that platform engineering becomes a network
of agents that each do their own job and collaborate.

He frames this as a new paradigm for platform engineering rather than a pile of single AI assistants,
and predicts that networked collaboration among agents will be a core trend for enterprise DevOps in
2026. The second half of the post turns from protocols to orchestration and describes the architecture
of [[SoftwareApplication/routa]] as a practical reference.

## Key Points

- The post claims, citing survey figures, that most enterprises have introduced several different AI
  agents while only a minority have achieved effective collaboration among them, and that the cost
  shows up as higher spending, longer delivery cycles from tool switching and lost context, and
  developers having to learn many interaction styles.
- It describes platform engineering's adoption of AI as five stages: manual requirements and planning,
  script automation, single-point AI assistants that only suggest, autonomous coding agents that read
  and write files and commit code, and finally agent networks in which multiple agents divide work
  under a unified protocol layer and an orchestration engine. The author places the industry in the
  transition from the fourth stage to the fifth.
- It assigns each protocol a layer, with an analogy for each: MCP standardises how an agent gets tools
  and context ("a USB port"), ACP manages a coding agent's process lifecycle from the IDE ("operating
  system process management"), and A2A handles discovery and collaboration between agents across
  platforms ("the internet's HTTP").
- From an orchestration point of view, the author says collaboration operations such as creating a
  sub-agent, delegating a task, messaging another agent and reporting to a parent can themselves be
  exposed as MCP tools, so any MCP-capable agent can call them.
- He treats a Skill not as a separate protocol but as a sub-concept of A2A and coding-agent systems: an
  A2A Skill announces externally what an agent can do, while an internal Skill holds an agent's role
  instructions and behavioural boundaries. An orchestration engine can then match tasks to agents by
  Skill, which he calls an agent's "capability résumé".
- He contrasts two orchestration modes. In external orchestration, an orchestrator outside the agents
  starts a coordinator agent over ACP, which splits the work and launches separate ACP agents for the
  subtasks; results flow back through an event bus. In the Workspace Agent mode, a single
  macro-coordinating ACP agent splits tasks and schedules sub-agents itself, managing their state
  internally. He lists process isolation, auditability and extensibility as strengths of the first,
  against process overhead and system complexity; and unified state and flexible macro-scheduling as
  strengths of the second, against single-point-of-failure risk.
- As a reference, he presents Routa as a hybrid of the two modes, with role boundaries for a
  coordinator that plans but does not write code, an implementor that does not widen task scope, and a
  verifier that reviews but does not modify code.
- He concludes that protocols are only the roads and orchestration is the traffic system: task
  decomposition, agent scheduling, event synchronisation and state management are what turn scattered
  agents into a schedulable, traceable network.

## Context

The post is the author's forecast and opinion piece combined with a description of an open-source
project linked from it. It reports no measurements of its own; the survey figures it quotes are
attributed to reports listed in its references. It belongs to a run of the author's writing on agent protocols and
multi-agent coding platforms, including [[BlogPosting/acp-protocol-and-multiple-ai-coding-agents]].
