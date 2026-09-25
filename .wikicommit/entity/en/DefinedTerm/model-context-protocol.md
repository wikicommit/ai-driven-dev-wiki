---
title: "Model Context Protocol"
type: "schema:DefinedTerm"
lang: en
aliases: ["MCP"]
tags: [agents, tool-use]
sources:
  - type: url
    url: https://arxiv.org/pdf/2602.15945
    hash: sha256:60c6e2cb0a71555099b80957589b805892374a300cde0b5fcf920cd270f4c095
  - type: url
    url: 'https://arxiv.org/pdf/2606.28791'
    hash: sha256:0de559cacdfe9078d48a08a5f2b05d76219a579abd307e3a72ca17d1894464d0
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/building-your-first-mcp-server-how-to-extend-ai-tools-with-custom-capabilities/'
    hash: sha256:79fe71c090476d29a3745d92b375a5354c83e43dff0abc079080c9c6d7048789
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A client-server protocol that standardizes how AI agents discover, select, and invoke external tools exposed by MCP servers, without specifying how much tool metadata or output must be exposed to the model."
---

Model Context Protocol (MCP) is a client-server protocol that standardizes how AI agents discover
and invoke external tools across heterogeneous execution environments. An MCP server exposes tool
metadata — names, input schemas, and descriptions — that an agent can query across multiple
connected servers; when the agent selects a tool, it issues a structured request, and the server
executes it and returns the result in serialized form.

## Usage

[[ScholarlyArticle/from-determinism-to-delegation]] describes the protocol's origin and role structure.
Connecting heterogeneous models to proprietary tools had historically required bespoke connectors, and
that paper describes MCP as replacing N times M custom integrations with a single client-server
contract. It names three roles: an **MCP Host** managing consent and policy, an **MCP
Client** connecting to individual servers, and an **MCP Server** exposing read-only **Resources**,
executable **Tools** validated by JSON Schema and gated by human approval, and reusable **Prompts**.
That paper's reading of why standardized tool protocols matter is structural: they are what allow
agents to discover and act upon the deterministic APIs that classical software engineering provides —
what it calls the technical seam of the symbiosis between the two disciplines.

A practitioner's account on GitHub's blog, [[BlogPosting/building-your-first-mcp-server]],
describes the same structure from the side of someone configuring and building servers. The host
is the AI tool in use — its example is [[SoftwareApplication/github-copilot]] in VS Code — and it
creates one client per server it connects to; registering a server with the host (in VS Code, a
`.vscode/mcp.json` entry naming the command that starts it) is what makes the server's capabilities
available to the agent. The post presents tools (actions the AI can take, each with a description
and input schema), resources (context the AI can read, often under a URI-based identifier) and
prompts (predefined guidance a server ships, surfaced in VS Code as slash commands) as the three
core server building blocks, and notes that the specification has since added further capabilities
including sampling and elicitation. Its practical advice is to look for an existing server before
building one, such as the [[SoftwareApplication/github-mcp-server]], and to vet third-party servers
as supply-chain dependencies — whether the publisher is recognizable and the code open to review.

The MCP standardizes tool interfaces but does not specify how much metadata and output must be
exposed to the model. A study of MCP execution models,
[[ScholarlyArticle/from-tool-orchestration-to-code-execution]], calls the traditional arrangement a
context-coupled execution model: existing implementations serialize tool metadata, full schemas and
tool outputs directly into the agent's reasoning context, where they compete for space with user
input and intermediate reasoning. That paper argues that as the number of connected servers and
available tools grows, this material consumes an increasing share of the context window, leaving
less capacity for reasoning and degrading performance on wide-context analytical tasks — so that
context-coupled execution does not scale with the size of the tool ecosystem.

The same paper sets out [[DefinedTerm/code-execution-mcp]] as an alternative, context-decoupled
execution model that addresses this limitation by decoupling tool orchestration from the agent's
context window.

## Related Terms

- [[DefinedTerm/code-execution-mcp]] — an alternative execution model for MCP that generates a
  single executable program instead of iteratively invoking tools through the context window
- [[ScholarlyArticle/from-tool-orchestration-to-code-execution]] — an empirical comparison of
  traditional MCP against Code Execution MCP on efficiency, task quality, and security
- [[ScholarlyArticle/from-determinism-to-delegation]] — source of the Host/Client/Server role structure
  and the N-times-M framing above
- [[BlogPosting/building-your-first-mcp-server]] — an introductory walkthrough of building an MCP
  server and registering it with GitHub Copilot in VS Code
