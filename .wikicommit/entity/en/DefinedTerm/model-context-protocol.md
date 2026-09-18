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
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

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
MCP — which that paper dates to late 2024 — replaces N times M custom integrations with a single
client-server contract. It names three roles: an **MCP Host** managing consent and policy, an **MCP
Client** connecting to individual servers, and an **MCP Server** exposing read-only **Resources**,
executable **Tools** validated by JSON Schema and gated by human approval, and reusable **Prompts**.
That paper's reading of why standardized tool protocols matter is structural: they are what allow
agents to discover and act upon the deterministic APIs that classical software engineering provides —
what it calls the technical seam of the symbiosis between the two disciplines.

The MCP standardizes tool interfaces but does not specify how much metadata and output must be
exposed to the model. In the traditional (context-coupled) execution model that most existing
implementations use, tool metadata, schemas, and outputs are all sent directly into the agent's
reasoning context, competing for space with user input and intermediate reasoning. As the number of
connected servers and available tools grows, this metadata and output can consume an increasing
share of the context window, leaving less capacity for reasoning and degrading performance on
wide-context analytical tasks — a scalability limitation this architecture does not overcome by
adding more servers or tools.

[[DefinedTerm/code-execution-mcp]] is an alternative execution model, introduced to address this
limitation by decoupling tool orchestration from the agent's context window.

## Related Terms

- [[DefinedTerm/code-execution-mcp]] — an alternative execution model for MCP that generates a
  single executable program instead of iteratively invoking tools through the context window
- [[ScholarlyArticle/from-tool-orchestration-to-code-execution]] — an empirical comparison of
  traditional MCP against Code Execution MCP on efficiency, task quality, and security
- [[ScholarlyArticle/from-determinism-to-delegation]] — source of the Host/Client/Server role structure
  and the N-times-M framing above
