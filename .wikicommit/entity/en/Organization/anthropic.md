---
title: "Anthropic"
type: "schema:Organization"
lang: en
tags: [agentic-coding, context-engineering]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf'
    hash: sha256:c63d41952636629543bbc11004c9be52b96f346284383c32bcd91f9130d25932
  - type: url
    url: 'https://www.anthropic.com/news/model-context-protocol'
    hash: sha256:e33f7635c7066ce5080d114a7e486537f8686757e5de41c7f480e0acd0b28da4
  - type: url
    url: 'https://en.wikipedia.org/wiki/Model_Context_Protocol'
    hash: sha256:f114caf967b13aa97382a0bea6ed771c920c8c79930883437e9a34df46e9c542
  - type: url
    url: 'https://www.anthropic.com/engineering/code-execution-with-mcp'
    hash: sha256:00595274b94dc84401f5d20a982fac4221bd6fef1a8b89c318ac7ad3122afaf8
  - type: url
    url: 'https://www.coalitionforsecureai.org/wp-content/uploads/2026/03/model-context-protocol-security-1.pdf'
    hash: sha256:d5ea586dbd65785c34ba7afa769d56a4d1bcc77eb7876b7578edff5516c979a5
  - type: url
    url: 'https://github.com/agentskills/agentskills'
    hash: sha256:62d24fa3cf7cabfa0348af3065f32a15c43faf2d30b3352ff41f02e3a2399faa
  - type: url
    url: 'https://www.anthropic.com/engineering/writing-tools-for-agents'
    hash: sha256:effc06d088266ee895582c23541e543435288246b1dc4d89d3a2f4b8a1993b54
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The company behind the Claude models and [[SoftwareApplication/claude-code]], the origin of [[DefinedTerm/model-context-protocol]], and a prolific publisher of practitioner writing on [[DefinedTerm/context-engineering]] and agentic coding."
  url: "https://www.anthropic.com/"
---

Anthropic is the company behind the Claude family of models and [[SoftwareApplication/claude-code]], its agentic coding tool. Alongside its products it publishes engineering writing and industry forecasts on how coding agents are used, which makes it both a vendor in the agentic coding space and one of the more visible sources of practitioner vocabulary for it.

## History

The sources ingested here do not cover Anthropic's founding or corporate history; they document its output on agentic coding from late 2024 onward.

The earliest event they record is the announcement of [[DefinedTerm/model-context-protocol]] on 25 November 2024, created at Anthropic by [[Person/david-soria-parra]] and [[Person/justin-spahr-summers]] and open-sourced as a standard for connecting AI assistants to the systems where data lives. In December 2025 Anthropic donated the protocol to the [[Organization/agentic-ai-foundation]], a directed fund under the Linux Foundation it co-founded with Block and [[Organization/openai]]; later that month it published [[DefinedTerm/agent-skills]] as a companion open standard for packaging task-specific instructions and resources that agents load on demand, following the same open-standard approach. The Agent Skills specification repository gives the same account of the format's origin from the standard's own side — originally developed by Anthropic, then released as an open standard — and records that it has since been adopted by a growing number of agent products and is open to contributions from the broader ecosystem, with repository code under Apache 2.0 and documentation under CC-BY-4.0.

## Activities & Products

Its engineering writing on agent design is published under an "Engineering at Anthropic" banner. [[TechArticle/effective-context-engineering-for-ai-agents]], published on 29 September 2025 by its Applied AI team, sets out the company's position that [[DefinedTerm/context-engineering]] is the natural progression of prompt engineering, and prescribes [[DefinedTerm/compaction]], structured note-taking, and sub-agent architectures for long-horizon tasks. That post describes several techniques by reference to how Claude Code implements them, including just-in-time file retrieval through glob and grep alongside `CLAUDE.md` loaded up front. A second post in the same series, [[TechArticle/writing-effective-tools-for-agents]] of 11 September 2025 by Ken Aizawa, applies the same reasoning to the tools an agent is given, and is notable for how the company says the advice was produced: most of it came from repeatedly optimizing Anthropic's own internal tool implementations with Claude Code, evaluated against its own internal workspace, with held-out test sets showing gains beyond implementations written by its researchers.

The company also publishes forecasts. [[Report/2026-agentic-coding-trends-report]] predicts eight trends for agentic coding in 2026 and reports internal research findings, including work from its Societal Impacts team finding that developers use AI in roughly 60% of their work while reporting they can "fully delegate" only 0–20% of tasks. That report also describes Anthropic's own internal use of Claude Code outside engineering — its legal team building Claude-powered workflows for contract redlining and content review, with a lawyer who had no coding experience building self-service triage tools.

Its protocol work is the widest-reaching of these. [[BlogPosting/introducing-the-model-context-protocol]] shipped MCP with a specification and SDKs, local server support in the Claude Desktop apps, and an open-source repository of servers, naming Block and Apollo as early adopters alongside development-tools companies Zed, Replit, Codeium and Sourcegraph. A year later [[TechArticle/code-execution-with-mcp]], by Adam Jones and Conor Kelly, addressed what that adoption had cost: with agents connected to hundreds or thousands of tools, loading every definition upfront and passing intermediate results through the model consumes excessive tokens. Its proposed answer is [[DefinedTerm/code-execution-with-mcp]], which it reports taking one example workflow from 150,000 tokens to 2,000.

Anthropic also appears in third-party security work on its own protocol. [[Report/model-context-protocol-security]] states that its authors are collaborating with Anthropic and the MCP maintainer community to keep the recommendations practical and implementable, and lists Anthropic-affiliated people among its editors, contributors and Technical Steering Committee co-chairs.

Its developer-facing platform features referenced in this writing include a memory tool and context management capabilities released in public beta on the Claude Developer Platform, and tool result clearing as a lightweight form of compaction.
