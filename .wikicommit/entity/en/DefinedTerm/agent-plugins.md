---
title: "Agent Plugins"
type: "schema:DefinedTerm"
lang: en
tags: [agent-tooling, agent-skills, mcp]
sources:
  - type: url
    url: 'https://developers.googleblog.com/agent-plugins-package-your-skills-tools-and-more/'
    hash: sha256:db0cfe6b242f1f7ec3c7efd7ead8d95b5da039f04572d7cbc8540fa6ee8545df
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An open, vendor-neutral specification for packaging agent skills and MCP servers together into one portable plugin directory that different agent clients can load."
---

Agent Plugins is an open, vendor-neutral specification for packaging [[DefinedTerm/agent-skills]] and [[DefinedTerm/model-context-protocol]] servers into portable plugins. A plugin is a directory with a fixed layout — a minimal `plugin.json` manifest naming the plugin, skills under `skills/`, MCP servers declared in `mcp.json` — plus an optional reverse-domain directory that a single client owns for its own additions. Version 1.0.0 was published by a technical steering committee of core maintainers from Amazon, Cursor, Microsoft, OpenAI and Vercel, and [[Organization/google]] announced in August 2026 that it was joining as a Core Maintainer.

## Usage

The problem the format addresses, as Google's announcement ([[BlogPosting/agent-plugins-package-your-skills-tools-and-more]]) puts it, is not the components but the box they ship in: skills and MCP servers were each already portable, while every client invented its own directory layout, manifest metadata and MCP configuration shape, forcing authors to fork a package per client. The specification fixes the parts that are the same everywhere and leaves room elsewhere. The manifest cannot relocate components or declare them inline; each `mcp.json` entry states its transport explicitly (stdio, Streamable HTTP or legacy HTTP+SSE), so a client never infers one from the shape of a configuration object; and components fail independently, so a server that does not start is skipped and reported while the plugin's skills still load. Hooks, agents, commands and other client-specific features go in the client's own namespace directory, which other clients ignore.

Version 1 is deliberately only a package format. It defines no install mechanism, distribution protocol, permission model, sandboxing requirement, trust or provenance verification, or user experience, leaving those to each client. Google's post places it in a layered ecosystem — discovery through Agentic Resource Discovery, catalogue entries through AI Catalog, packaging through Agent Plugins, and execution through MCP and Agent Skills — each adoptable on its own. Google names [[SoftwareApplication/agents-cli]] and Data Agent Kit as its first products supporting the format.

## When It Applies

According to the announcement, a plugin is worth using only when several components belong together and need to travel together. A single MCP server shipped to a single client is still simpler as an `mcp.json` alone, and a single skill does not need a plugin. Everything described here comes from one vendor's announcement of a specification it had just joined; it states the design and intent, not adoption or interoperability that has been measured.

## Related Terms

- [[DefinedTerm/agent-skills]]
- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agent-hooks]]
