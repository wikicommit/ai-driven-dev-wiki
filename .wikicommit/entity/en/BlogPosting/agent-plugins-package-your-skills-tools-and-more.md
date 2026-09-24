---
title: "Agent Plugins package your skills, tools, and more"
type: "schema:BlogPosting"
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
  description: "Google's announcement that it is joining the Agent Plugins specification as a Core Maintainer, with an explanation of what the format packages, what it deliberately leaves out, and where it sits among neighbouring agent standards."
  author: ["Kevin Hou", "Haoyu Wang", "Alan Blount"]
  datePublished: "2026-08-06"
  publisher: "[[Organization/google]]"
---

This post announces that [[Organization/google]] is joining [[DefinedTerm/agent-plugins]] as a Core Maintainer and starting to build support for it into its own products. It describes Agent Plugins 1.0.0 as an open, vendor-neutral specification for packaging [[DefinedTerm/agent-skills]] and [[DefinedTerm/model-context-protocol]] servers into portable plugins, published by a technical steering committee of core maintainers from Amazon, Cursor, Microsoft, OpenAI and Vercel.

The argument turns on where portability breaks down. A skill and the MCP server that goes with it are each portable on their own, the post says, but the wrapper around them is not: each client expects a different directory layout, manifest metadata and MCP configuration shape, so an author shipping to a second client ends up forking the package and maintaining copies that drift. Its diagnosis is that "the core problem isn't the components. It's the manifest."

## Key Points

- A plugin is a directory: a `plugin.json` manifest whose only substance is a schema reference and a name, skills under `skills/` in the Agent Skills format, and MCP servers declared in `mcp.json` with an explicit transport type on every entry.
- The manifest cannot relocate components or declare them inline, so there is no discovery path to configure and no precedence order to learn.
- Components fail independently: a client loads whatever is present, and an MCP server that fails to start is skipped and reported without taking the plugin's skills down with it.
- A reverse-domain directory (for example `com.example.client/`) is a namespace owned by one client, for hooks, agents, commands or anything else it wants to add; other clients ignore it. The post presents this as what keeps the portable core small.
- Not everything should be a plugin: a single MCP server for a single client, or a single skill, does not need one. The format is for components that belong and travel together.
- Version 1 is a package format and nothing more — it defines no install mechanism, distribution protocol, permission model, sandboxing, trust or provenance verification, or user experience. The post calls this the right call because those obligations differ between an IDE, a CLI and a managed enterprise platform, and notes that the project names them openly as future considerations.
- The post separates four layers — find (Agentic Resource Discovery), describe (AI Catalog), package (Agent Plugins) and run (MCP and Agent Skills) — and says each can be adopted independently of the others.
- [[SoftwareApplication/agents-cli]] and Data Agent Kit are named as the two Google products supporting the format on the day of publication, and more are expected.

## Context

This is Google's account of a specification it has just joined, written by its own engineers and product managers, so it explains the format's design and Google's reasons for backing it rather than reporting any measured adoption. It closes on the position that packaging is "unglamorous infrastructure" that should be shared rather than reinvented by each client.
