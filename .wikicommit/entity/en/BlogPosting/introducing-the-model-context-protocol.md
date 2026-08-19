---
title: "Introducing the Model Context Protocol"
type: "schema:BlogPosting"
lang: en
tags: [mcp, agentic-coding]
sources:
  - type: url
    url: 'https://www.anthropic.com/news/model-context-protocol'
    hash: sha256:e33f7635c7066ce5080d114a7e486537f8686757e5de41c7f480e0acd0b28da4
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Anthropic's announcement of 25 November 2024 open-sourcing the Model Context Protocol, naming its three launch components, its early adopters, and its two creators."
  datePublished: "2024-11-25"
  publisher: "[[Organization/anthropic]]"
---

"Introducing the Model Context Protocol" is the announcement post, dated 25 November 2024, in which [[Organization/anthropic]] open-sourced [[DefinedTerm/model-context-protocol]] as "a new standard for connecting AI assistants to the systems where data lives, including content repositories, business tools, and development environments." Its stated aim is to help frontier models produce better, more relevant responses.

The post's argument for why a standard was needed rests on a mismatch: the industry had invested heavily in model capabilities and achieved rapid advances in reasoning and quality, yet even the most sophisticated models remained constrained by isolation from data — "trapped behind information silos and legacy systems" — with every new data source requiring its own custom implementation, making truly connected systems hard to scale. MCP is presented as replacing those fragmented integrations with a single protocol, described architecturally as straightforward: developers either expose their data through MCP servers or build AI applications (MCP clients) that connect to those servers.

## Key Points

- Three components shipped at launch: the specification and SDKs, local MCP server support in the Claude Desktop apps, and an open-source repository of MCP servers.
- Pre-built servers were published for Google Drive, Slack, GitHub, Git, Postgres and Puppeteer, and the post states that Claude 3.5 Sonnet is adept at quickly building MCP server implementations.
- Named early adopters were Block and Apollo, with development tools companies Zed, Replit, Codeium and Sourcegraph working with MCP to enhance their platforms — the stated benefit being that AI agents can better retrieve relevant information to understand the context around a coding task and produce more nuanced, functional code with fewer attempts.
- Dhanji R. Prasanna, Chief Technology Officer at Block, is quoted saying that "open technologies like the Model Context Protocol are the bridges that connect AI to real-world applications, ensuring innovation is accessible, transparent, and rooted in collaboration," and that Block was excited to use it to build agentic systems that "remove the burden of the mechanical so people can focus on the creative."
- The forward-looking claim is architectural rather than about features: as the ecosystem matures, AI systems will maintain context as they move between different tools and datasets, replacing fragmented integrations with a more sustainable architecture.
- On availability at launch, all Claude.ai plans supported connecting MCP servers to the Claude Desktop app, Claude for Work customers could test servers locally against internal systems, and Anthropic said it would soon provide developer toolkits for deploying remote production servers.
- The post credits the protocol's creation: "MCP was created at Anthropic by [[Person/david-soria-parra]] and [[Person/justin-spahr-summers]]."

## Context

The post closes on an explicitly open-community framing — a commitment to building MCP as a collaborative, open-source project and ecosystem, and an invitation to AI tool developers, enterprises with existing data, and early adopters alike. That framing is worth reading as a starting position rather than a settled one: the same protocol was later donated to an independent foundation, and its security properties became the subject of independent analysis. Both developments are covered on [[DefinedTerm/model-context-protocol]].
