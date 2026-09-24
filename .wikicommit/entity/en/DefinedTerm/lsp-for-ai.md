---
title: "LSP for AI"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-engineering, tool-use, mcp]
sources:
  - type: url
    url: 'https://addyosmani.com/agentic-engineering/lsp-for-ai/'
    hash: sha256:57f4e0030e951e4a6fa96f4d49d45eb81be2ebd4cb64d018640e0c22b02209d9
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The idea that AI coding tools need a shared integration standard with developer tools, in the way the Language Server Protocol let one language server work with any editor that speaks it."
---

"LSP for AI" is the idea that AI coding tools need a shared standard for integrating with developer tools, by analogy with the Language Server Protocol (LSP). Before LSP, every code editor had to build its own support for every programming language; a language server written once now works with any editor that speaks LSP, turning an M×N integration problem into an M+N one. Addy Osmani's agentic engineering glossary describes AI coding assistants as facing the same M×N problem today, each building its own ways to read code, run tests and search documentation, and presents a standard protocol through which any AI client can talk to any tool server as the equivalent fix.

## Usage

The glossary treats protocols such as the [[DefinedTerm/model-context-protocol]] as early steps toward this vision, and calls Anthropic's MCP the most widely adopted AI tool protocol at the time of writing. The benefits it claims for engineers working with an [[DefinedTerm/ai-coding-agent]] are less lock-in to any one AI tool — swapping AI providers without rebuilding integrations — and better tooling overall, because a well-built server, for example an MCP server for GitHub or for a database, then serves every compatible client instead of a single one. It draws the parallel that LSP's standardization led to an explosion of high-quality language tooling.

The glossary describes the vision as still early and evolving, and expects current protocols to iterate significantly as the field matures.

## Related Terms

- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/ai-coding-agent]]
