---
title: "Anthropic"
type: "schema:Organization"
lang: en
tags: [agents, llm]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The company behind the Claude models, the agentic coding tool Claude Code, and the Claude Developer Platform, and the publisher of the Engineering at Anthropic blog."
  url: "https://www.anthropic.com/"
---

Anthropic is the company behind the Claude family of models and the tools built on them,
including the agentic coding solution [[SoftwareApplication/claude-code]] and the Claude Developer
Platform. It publishes engineering guidance for teams building agents on Claude through its
Engineering at Anthropic blog.

Its Applied AI team writes on building agents in practice. That team's stated position is that
[[DefinedTerm/context-engineering]] is the natural progression of
[[DefinedTerm/prompt-engineering]], and that context should be treated as a finite resource to be
curated rather than filled — a view set out in
[[BlogPosting/effective-context-engineering-for-ai-agents]]. Anthropic gives "do the simplest
thing that works" as its standing advice for teams building agents on top of Claude.

A post on long-running agents describes two further pieces of Anthropic's published engineering work: a two-agent harness for autonomous full-stack development (an initializer agent that sets up a project once, and a coding agent woken up repeatedly to make incremental progress, run tests, and commit), and the [[DefinedTerm/brain-hands-session-split]] architecture behind [[SoftwareApplication/claude-managed-agents]]. The same post describes Anthropic's Project Vend, in which a Claude instance ran an actual office vending business for a month, as an early public demonstration of what happens when an agent has to maintain a coherent identity across weeks rather than single sessions, and cites a separate scientific-computing case study in which Claude Opus 4.6 built a Boltzmann solver over a few days that reached sub-percent agreement with a reference implementation.

## Activities & Products
- The Claude family of models.
- [[SoftwareApplication/claude-code]], its agentic coding solution.
- The Claude Developer Platform, on which Anthropic has released a memory tool in public beta for
  storing and consulting information outside the context window through a file-based system, and a
  tool result clearing feature.
- [[SoftwareApplication/claude-managed-agents]], its hosted runtime for long-running agents.
- Engineering at Anthropic, the blog on which it publishes guidance for developers.
