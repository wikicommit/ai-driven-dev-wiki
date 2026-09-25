---
title: "Kimi CLI"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, cli]
sources:
  - type: url
    url: 'https://github.com/MoonshotAI/kimi-cli'
    hash: sha256:9d2248185093cc2e4853401a2af17466ff68fb53e2b1b88ca967e866a56f0bdc
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Moonshot AI's Python AI agent for the terminal, which helped with software development tasks and terminal operations by reading and editing code, running shell commands and searching and fetching web pages. Its repository has been archived and the tool replaced by Kimi Code CLI."
  applicationCategory: "Terminal coding agent"
  author: "Moonshot AI"
---

Kimi CLI is an AI agent that runs in the terminal, published by Moonshot AI under the Apache License 2.0, to help complete software development tasks and terminal operations. According to its README it can read and edit code, execute shell commands, search and fetch web pages, and autonomously plan and adjust its actions during execution.

The repository has been archived and is read-only. Its README states that the Python Kimi CLI has been replaced by Kimi Code CLI, described as the next-generation terminal AI agent from the same team; that there will be no further releases, bug fixes or security updates; and that existing installations are no longer supported and will stop working. On first launch, Kimi Code CLI detects Kimi CLI's data and offers to migrate its configuration, MCP servers, input history and sessions, while login credentials, MCP authorizations and Kimi CLI plugins are not migrated. The other packages published from the same repository — kosong, pykaos, kimi-sdk, and a PyPI package named kimi-code that is a legacy alias of kimi-cli rather than the new tool — were archived with it.

## Capabilities

The features below are those described in the original README, which the archived repository keeps for reference.

Kimi CLI presents itself as a shell as well as a coding agent: pressing Ctrl-X switches to a shell command mode in which shell commands run directly without leaving the tool, although built-in shell commands such as `cd` were not yet supported. A Zsh plugin works the other way round, letting a Zsh session switch into agent mode with the same key. The agent integrates with Visual Studio Code through the Kimi Code VS Code extension, and supports the Agent Client Protocol out of the box, so any ACP-compatible editor or IDE — the README's examples are Zed and JetBrains IDEs — can start it as an agent server with `kimi acp` and run Kimi CLI threads in the IDE's agent panel.

It supports [[DefinedTerm/model-context-protocol]] tools. A `kimi mcp` sub-command group adds servers over streamable HTTP (optionally with OAuth authorization) or stdio, and lists, removes and authorizes them; alternatively, a configuration file in the common MCP config format can be passed with `--mcp-config-file` to connect to servers for a single run.
