---
title: "BMAD (Breakthrough Method for Agile AI-Driven Development)"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, multi-agent-systems]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A multi-agent framework, published on GitHub, that organizes AI agents into agile roles — Product Owner, Architect, Developer, Tester — to tackle software projects through up-front planning, task sharding into focused 'story files,' and parallel specialized-agent execution."
  applicationCategory: "Multi-agent AI development framework"
  featureList: "Up-front agentic planning producing PRDs and designs; Scrum-like sharding into story files with focused context; parallel execution by specialized role agents (Product Owner, Architect, Developer, Tester)"
---

BMAD (Breakthrough Method for Agile AI-Driven Development) is a multi-agent framework, published on GitHub, that [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] cites twice: as "a more comprehensive example" of engineered multi-agent teams than Anthropic's Claude Code (whose architecture shifted from a monolithic agent to spawning specialized sub-agents), and separately as "a comprehensive industry example" of its [[DefinedTerm/ai-teammate-lifecycle-engineering]] (Lifetime Teammates) principles. It organizes agents into agile roles — Product Owner, Architect, Developer, Tester — taking the "team" metaphor literally to tackle complex projects within a full-fledged agile structure.

## Capabilities

Up-front agentic planning yields PRDs and designs; a Scrum-like sharding step then creates "story files" holding focused context for a task; specialized agents execute these in parallel. The paper credits BMAD's role specialization, task sharding, and high parallelism as mapping well to [[DefinedTerm/structured-agentic-software-engineering]] (SASE)'s own N-version programming and orchestration.

## Adoption & Ecosystem

The paper contrasts BMAD with its own proposed SASE, stating SASE goes further by converting review feedback into persistent [[DefinedTerm/mentorscript]] rules ("mentorship-as-code") and by specifying dedicated environments and disciplines — the [[DefinedTerm/agent-command-environment]] for human coaching and orchestration, the [[DefinedTerm/agent-execution-environment]] for agent execution, and [[DefinedTerm/ai-teammate-lifecycle-engineering]]/[[DefinedTerm/ai-teammate-infrastructure-engineering]] for memory, lifecycle, and agent-native tooling.
