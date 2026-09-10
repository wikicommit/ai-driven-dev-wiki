---
title: "Anthropic"
type: "schema:Organization"
lang: en
tags: [agents, llm]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

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

## Activities & Products
- The Claude family of models.
- [[SoftwareApplication/claude-code]], its agentic coding solution.
- The Claude Developer Platform, on which Anthropic has released a memory tool in public beta for
  storing and consulting information outside the context window through a file-based system, and a
  tool result clearing feature.
- Engineering at Anthropic, the blog on which it publishes guidance for developers.
