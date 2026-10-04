---
title: "AI Coding Fluency"
type: "schema:DefinedTerm"
lang: en
tags: [maturity-models, human-ai-collaboration, agentic-coding, context-engineering]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/ai-coding-fluency/'
    hash: sha256:67d5b1a10a94b426a6f03839b39167f5edbd52c14f1c2094a47d995b4dae0329
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A model proposed by Phodal Huang, adapted from the Agile Fluency Model, that describes how a team's capability to develop software with AI evolves across five levels — Awareness, Assisted Coding, Structured AI Coding, Agent-Centric and Agent-First — along five dimensions of collaboration, lifecycle coverage, engineering harness, governance and context."
---

AI Coding Fluency is a model, proposed by Phodal Huang in a March 2026 blog post, that treats AI programming as a set of team capabilities that evolve over time rather than as a one-off tool adoption. Borrowing the idea of the Agile Fluency Model, it describes five levels — **Awareness**, **Assisted Coding**, **Structured AI Coding**, **Agent-Centric** and **Agent-First** — each characterised along five dimensions: human-AI collaboration, software development lifecycle (SDLC) coverage, the AI engineering harness, governance and quality, and [[DefinedTerm/context-engineering]]. Across the levels the developer's role shifts from asking an AI questions, to delegating tasks defined by a spec, to decomposing goals and building the environment in which agents do the execution, and finally to verifying the system's leverage and business value while agents work end to end.

## Usage

The post lays the model out as a table. At **Awareness**, developers ask and the AI answers through a standalone chat interface, review is entirely manual and context is a single conversation. At **Assisted Coding**, the developer still leads while an IDE plugin completes and predicts code, quality relies on traditional linters and formatters with humans guarding against hallucination, and context is the active file and nearby tabs. At **Structured AI Coding**, the developer defines a spec and the AI helps generate whole modules, an IDE or CLI agent is wired to CI with automatic feedback, static analysis and test-coverage gates block changes, and retrieval reaches the repository and its history of issues and pull requests. At **Agent-Centric**, humans focus on decomposing goals and building the environment, agents also manage CI/CD and monitoring dashboards, they are given local observability and UI control, architectural boundaries are enforced with agent-specific linters, and the repository itself is the record, organised as a directory map with progressive disclosure. At **Agent-First**, humans no longer write code by hand, agents autonomously reproduce bugs, fix them, verify the fixes and merge the pull requests end to end with multi-round agent-to-agent review, background agents periodically clean up code entropy and technical debt, and a dedicated knowledge agent generates and maintains the system's memory.

The model is presented as a lens for understanding which direction a team's AI programming capability is developing in, not as a measure of organisational maturity. The post frames the challenges it addresses — trust in large volumes of generated code, the AI's dependence on context about architecture, dependencies and business rules, and the design of tasks an AI can understand and execute — as problems of collaboration rather than of model capability, and compares the shift to the Digital Fluency Model's view that what matters is an organisation's capability to create value with technology rather than the technology itself. See also [[DefinedTerm/ai-maturity-levels]], a different level-based model of AI adoption in product-development teams.

## When It Applies

The author states that, like other fluency models, it is not a strict maturity path: different teams may hold capabilities from different levels at the same time, and its purpose is to help teams see the direction of travel rather than to grade them. It assumes the team is already using AI in development and asks how that use is organised — human-AI collaboration patterns, engineering-system support, quality governance and context management — rather than which tool is used. It is one practitioner's proposal in a single blog post, built by analogy with the Agile Fluency and Digital Fluency models rather than from measured data.

## Related Terms

- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/ai-maturity-levels]]
