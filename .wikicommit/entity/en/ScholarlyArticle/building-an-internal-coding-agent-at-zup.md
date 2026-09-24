---
title: "Building an Internal Coding Agent at Zup: Lessons and Open Questions"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, experience-report, tool-use, human-oversight]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.09805'
    hash: sha256:5548448f214c19ad5dc00da7e4b9ed77e7fb54d513d2f28b99d158836e1aea88
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An experience report on CodeGen, an internal coding agent at Zup Innovation, arguing that tool design, cross-tool safety guardrails and progressive human oversight mattered more to its reliability and adoption than model choice or prompt engineering."
  author: ["Gustavo Pinto", "Pedro Eduardo de Paula Naves", "Ana Paula Camargo", "Marselle Silva"]
  abstract: "The paper argues that enterprise teams building internal coding agents face a gap between prototype performance and production readiness because tool design, safety enforcement, state management and human trust calibration are as decisive as model quality, yet underreported. It presents CodeGen, an internal coding agent at Zup, and shows that targeted tool design and layered safety guardrails improved agent reliability more than prompt engineering, while progressive human oversight modes drove organic adoption without mandating trust."
  keywords: ["coding agents", "tool design", "guardrails", "human oversight", "enterprise"]
---

This paper reports on CodeGen, an [[DefinedTerm/ai-coding-agent]] built and deployed inside the
Brazilian company Zup Innovation for its enterprise software teams. It began as a proof of concept by two
members of the development team, at a time when the company's flagship developer platform, StackSpot
AI, offered IDE extensions that could suggest code but not act in the environment. Built deliberately
outside that platform's codebase and release cycle, the prototype gradually became a production
system used daily by developers. The authors' premise is that existing literature on coding agents
concentrates on model-level performance — benchmarks, prompting and reasoning strategies — while the
engineering decisions that decide whether an agent succeeds in production are rarely reported.

CodeGen follows the [[DefinedTerm/react-prompting]] pattern: given a natural-language prompt, it
reasons, selects and invokes tools, observes the results and iterates until done. It has three
components: a Node.js CLI that handles user interaction and executes tools locally on the developer's
machine, chosen because every major IDE already embeds a terminal; a FastAPI backend handling
authentication, routing, WebSocket connections for executors and Server-Sent Events for web portals;
and Maestro, an orchestration engine that runs the agentic loop by sending the model the system
prompt, history, bootstrap metadata about the environment and a tool manifest, relaying any requested
tool call to the CLI and feeding the result back until the model answers in text. Session state lives
in PostgreSQL with Redis as cache and messaging layer, interrupted tasks can be resumed, and a durable
event timeline records every tool call, model response and state transition.

The paper catalogues 13 design decisions across architecture and frameworks, tool design and safety,
and human oversight, each paired with its trade-off and lesson, and closes with six open questions.

## Key Points

- The authors report that refining tool descriptions, parameter schemas and error contracts produced
  more consistent improvements in agent reliability than prompt engineering alone, and argue that
  tool specification deserves the same rigour as API design.
- The edit tool performs targeted string replacement rather than whole-file rewrites, because models
  tend to truncate or omit content when regenerating long files; a read-before-edit policy, enforced
  through the system prompt rather than the tool itself, guards against edits to stale or imagined
  file content.
- The shell tool is described as both the most useful and the most dangerous tool, and is governed
  by layered [[DefinedTerm/guardrails]]: it can be disabled outright, specific commands can be blocked
  through configuration, an approval mode can require confirmation of every invocation, and all
  executions are logged.
- Safety turned out to be a system-level property: blocking one capability, such as direct file
  deletion, was ineffective while an unrestricted shell could achieve the same effect, so policies
  had to be applied consistently across the whole tool manifest.
- Developers began in approval mode, where edits and shell commands need confirmation, and moved to
  autonomous mode at their own pace as confidence grew; the authors treat such
  [[DefinedTerm/human-in-the-loop]] mechanisms as transitional scaffolds, and see the same
  progressive-exposure pattern in the dev–staging–production deployment pipeline for agent changes.
- A dedicated planning mode, which presents an action plan for the user to review before execution,
  was added because single-pass execution proved problematic for complex or high-stakes tasks.
- An early attempt with [[SoftwareApplication/langchain]] was abandoned because its original
  unidirectional chain model fitted the cyclical tool-calling loop poorly; the team implemented the
  loop by hand, and is now transitioning to modern orchestration abstractions after finding that newer
  ones such as [[SoftwareApplication/langgraph]] closely resemble what it had already built — which the
  authors read as validating a build-first, adopt-later strategy.
- Reasoning is delegated to the model, tuned through a thinking-effort setting, while the
  orchestrator enforces stop criteria, tool ordering, error handling and guardrails; the authors argue
  that stronger models reduce hand-coded logic but do not remove the need for orchestration.

## Notes

The open questions the authors pose concern how tool manifests should be designed to minimize misuse,
where the boundary between model-delegated reasoning and orchestrator-enforced control should lie,
how safety policies can be specified consistently across tools with overlapping capabilities, what
adaptive trust models could replace a binary switch between approval and autonomous modes, how
long-term cross-session memory should be structured, and how agent-generated code should enter quality
assurance pipelines as agents take on larger changes. They also frame most of their decisions as
explicit trade-offs — for example approval modes adding friction, and delegated reasoning reducing
deterministic control — rather than optimizations of a single metric.

The paper appears in the 1st AI Agent Journal (2026);
the version extracted here is arXiv:2604.09805v1 [cs.SE].
