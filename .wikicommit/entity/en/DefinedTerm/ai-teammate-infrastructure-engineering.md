---
title: "AI Teammate Infrastructure Engineering (ATIE)"
type: "schema:DefinedTerm"
lang: en
tags: [sase]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The engineering activity proposed in Structured Agentic Software Engineering (SASE) for building the agent-native toolchain and execution environment agents need — machine-readable protocols, structured diagnostics, and semantic search, in place of tools built for human cognition."
---

AI Teammate Infrastructure Engineering (ATIE) is one of the structured engineering activities proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] as part of [[DefinedTerm/structured-agentic-software-engineering]] (SASE), paired there with [[DefinedTerm/ai-teammate-lifecycle-engineering]] (ATLE) under the umbrella of "SE for Agents." Its stated purpose is to engineer the agent's environment — the [[DefinedTerm/agent-execution-environment]] (AEE) — and build the agent-native toolchains agents need to operate effectively.

## Usage

The paper argues tools built for human developers are often ill-suited for agents, because decades of SE tooling (IDEs, visual debuggers) reduce cognitive overload that agents do not need — shifting the optimization goal from "precision@K for a small K" (because human time is precious) to "precision@100" being acceptable when a subordinate agent can post-process the results. It points to Rust's toolchain — whose rich, constructive compiler messages let agents learn quickly from failures — as a blueprint for agent-friendly environments, and calls for agent-native Model Context Protocol (see [[DefinedTerm/model-context-protocol]]) servers that return deep, interpretable feedback and support agent-driven refinement of tool-usage descriptions, citing Anthropic's own manual optimization of its MCP descriptions for agents rather than humans as an early example of this kind of self-improving tooling loop. The paper's research roadmap for ATIE also covers the post-IDE human-agent interface (moving toward interfaces for orchestration, review, and structured mentorship as agents perform more direct editing) and distributed compute fabrics for agents (runtime support for isolation, reproducibility, scheduling, and cost control, with a declarative [[DefinedTerm/loopscript]] exposing workflow structure for optimization).

## Related Terms

[[DefinedTerm/ai-teammate-lifecycle-engineering]], [[DefinedTerm/agent-execution-environment]], [[DefinedTerm/model-context-protocol]]
