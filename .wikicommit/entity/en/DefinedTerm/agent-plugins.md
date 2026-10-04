---
title: "Agent Plugins"
type: "schema:DefinedTerm"
lang: en
tags: [agent-tooling, agent-skills, mcp]
sources:
  - type: url
    url: 'https://developers.googleblog.com/agent-plugins-package-your-skills-tools-and-more/'
    hash: sha256:db0cfe6b242f1f7ec3c7efd7ead8d95b5da039f04572d7cbc8540fa6ee8545df
  - type: url
    url: 'https://github.blog/changelog/2026-08-12-agent-plugins-1-0-in-vs-code-copilot-cli-and-the-copilot-app/'
    hash: sha256:be6d82bc0689096bdb35d44119285193d58cc31d2ba9d961c7cfd09646a2483b
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An open, vendor-neutral specification for packaging agent skills and MCP servers together into one portable plugin directory that different agent clients can load."
---

Agent Plugins is an open, vendor-neutral specification for packaging [[DefinedTerm/agent-skills]] and [[DefinedTerm/model-context-protocol]] servers into portable plugins. A plugin is a directory with a fixed layout — a minimal `plugin.json` manifest naming the plugin, skills under `skills/`, MCP servers declared in `mcp.json` — plus an optional reverse-domain directory that a single client owns for its own additions. Version 1.0.0 was published by a technical steering committee of core maintainers from Amazon, Cursor, Microsoft, OpenAI and Vercel, and [[Organization/google]] announced in August 2026 that it was joining as a Core Maintainer.

## Usage

The problem the format addresses, as Google's announcement ([[BlogPosting/agent-plugins-package-your-skills-tools-and-more]]) puts it, is not the components but the box they ship in: skills and MCP servers were each already portable, while every client invented its own directory layout, manifest metadata and MCP configuration shape, forcing authors to fork a package per client. The specification fixes the parts that are the same everywhere and leaves room elsewhere. The manifest cannot relocate components or declare them inline; each `mcp.json` entry states its transport explicitly (stdio, Streamable HTTP or legacy HTTP+SSE), so a client never infers one from the shape of a configuration object; and components fail independently, so a server that does not start is skipped and reported while the plugin's skills still load. Hooks, agents, commands and other client-specific features go in the client's own namespace directory, which other clients ignore.

Version 1 is deliberately only a package format. It defines no install mechanism, distribution protocol, permission model, sandboxing requirement, trust or provenance verification, or user experience, leaving those to each client. Google's post places it in a layered ecosystem — discovery through Agentic Resource Discovery, catalogue entries through AI Catalog, packaging through Agent Plugins, and execution through MCP and Agent Skills — each adoptable on its own. Google names [[SoftwareApplication/agents-cli]] and Data Agent Kit as its first products supporting the format.

GitHub's account of the same release, in a changelog entry of 12 August 2026, says GitHub published Agent Plugins 1.0 on 6 August together with AWS, Anysphere, Microsoft, OpenAI and Vercel, with Google joining as a core maintainer the same day; it describes the result as an open standard governed independently of any single vendor. That entry announces general availability of support in VS Code, [[SoftwareApplication/github-copilot-cli]], the GitHub Copilot SDK and the GitHub Copilot app on all Copilot plans. For an existing plugin, GitHub calls adopting the specification mostly manifest work: add `$schema` to `plugin.json`, keep skills under `skills/` and MCP configuration in `mcp.json`, and move Copilot-specific files into a `com.github.copilot/` directory that other clients ignore. Custom agents, commands, rules and hooks load from that directory across VS Code, Copilot CLI and the Copilot app, which is how, in GitHub's words, one package stays portable while keeping its Copilot behaviour. GitHub also states that its existing Copilot plugins that do not target the specification remain supported with no migration required.

The same entry addresses governance, which the specification itself leaves to clients. Copilot Business and Enterprise customers manage these plugins through the enterprise managed settings they already use: in `managed-settings.json`, `enabledPlugins` automatically installs or blocks specific plugins, `extraKnownMarketplaces` adds marketplaces available to developers, and `strictKnownMarketplaces` restricts installation to managed marketplaces. Enterprise values set a baseline, team-specific overrides combine with it additively, and no separate Agent Plugins policy is needed. Because a plugin can carry MCP server configurations, GitHub suggests pairing this with MCP allowlists that approve or block individual servers by URL, command or name.

## When It Applies

According to the announcement, a plugin is worth using only when several components belong together and need to travel together. A single MCP server shipped to a single client is still simpler as an `mcp.json` alone, and a single skill does not need a plugin. Everything described here comes from vendors' own announcements — Google's on joining the specification and GitHub's on shipping support for it; they state design, intent and availability, not adoption or interoperability that has been measured.

## Related Terms

- [[DefinedTerm/agent-skills]]
- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agent-hooks]]
