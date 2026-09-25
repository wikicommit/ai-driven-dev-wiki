---
title: "Cline"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-agents, coding-tools, open-source, cli, mcp]
sources:
  - type: url
    url: 'https://github.com/cline/cline'
    hash: sha256:72fd143bfd79de2aef9aff080275f161baa42b60162c7a665aeea8679ae24199
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source coding agent from Cline Bot Inc. that runs as a VS Code extension, a JetBrains plugin, a CLI and a desktop app on one shared agent engine, which is also published as an SDK for building custom agents."
  applicationCategory: "Coding agent"
  author: "Cline Bot Inc."
---

Cline is an open-source coding agent, published under the Apache 2.0 license by Cline Bot Inc., that
describes itself as "the open source coding agent in your IDE, terminal, & desktop." It ships in
several forms that share one agent core: a VS Code extension, a plugin for the JetBrains family of IDEs,
a command-line interface that can run interactively or fully headless, and a native desktop app for
macOS and Windows. The same engine is exposed as a Node.js SDK for building custom agents and
integrations. The repository holds the SDK, the CLI, the VS Code extension and the desktop app, while
the JetBrains plugin, which talks to the shared agent core, is not open-sourced.

## Capabilities

Cline reads a project's structure and makes coordinated changes across files, watching linter and
compiler errors as it goes so that it can fix problems such as missing imports and type mismatches.
In the IDE clients each edit appears as a diff the developer can review, modify or revert, and changes
are tracked with checkpoints so the agent's work can be undone. It runs shell commands in the terminal
and watches their output; for long-running processes such as development servers it keeps working in
the background and reacts to new output as it appears.

Work is split between a **Plan mode**, in which Cline explores the codebase, asks clarifying questions
and lays out a strategy, and an **Act mode**, in which it carries the plan out. By default every file
edit and terminal command needs the developer's approval, which the README presents as the way the
developer stays in control ([[DefinedTerm/human-in-the-loop]]); an auto-approve toggle lets it run
autonomously instead. Project-specific rules — coding standards, architecture conventions,
deployment procedures, testing requirements — live in `.clinerules` files that the CLI and both IDE
clients pick up automatically, and skills let the model load specific rules only when they are needed.

Cline is not tied to one model provider: the README lists Anthropic, OpenAI and Google models,
OpenRouter, the Vercel AI Gateway, AWS Bedrock, Azure and GCP Vertex, Cerebras and Groq, local models
through Ollama or LM Studio, and any OpenAI-compatible API. It is extended through plugins, which use
the SDK to register tools and lifecycle hooks for purposes such as logging, auditing and policy
enforcement, or through [[DefinedTerm/model-context-protocol]] servers, which the CLI manages with
`cline mcp`.

Beyond single sessions, the README describes multi-agent teams, in which a coordinator agent breaks
work into subtasks and delegates them to specialist agents that each have their own tools and context,
with team state persisting across sessions; scheduled agents that run on cron schedules independently
of any terminal session, for recurring jobs such as daily pull-request summaries; and connectors that
let a user talk to an agent from Telegram, Slack, Discord, Google Chat, WhatsApp or Linear, each
conversation thread mapping to one agent session. The headless CLI accepts piped input and can emit
JSON, for use in scripts and CI/CD pipelines.

## Adoption & Ecosystem

The VS Code extension is distributed through the Visual Studio Marketplace and the JetBrains plugin
through the JetBrains Marketplace, covering IntelliJ IDEA, PyCharm, WebStorm, GoLand and the rest of
that family. The CLI installs from npm as `cline` and the SDK as `@cline/sdk`. The desktop app is
built as a Tauri shell with a Bun sidecar and a Next.js interface, and lets the user run agent sessions
in any folder, schedule routines, and manage models, plugins and MCP servers.
