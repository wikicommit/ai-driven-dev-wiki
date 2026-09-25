---
title: "Taskmaster"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-tools, agent-tooling, mcp, cli, spec-driven-development]
sources:
  - type: url
    url: 'https://github.com/eyaltoledano/claude-task-master'
    hash: sha256:e86fbfd3ce08ae321ee5c557fdd924374c87be6a44ccc92505156ded24b179e2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A task-management system for AI-driven development that parses a product requirements document into structured tasks an AI coding assistant can plan, expand and work through, run either as an MCP server inside an AI editor or as the `task-master` command-line tool."
  applicationCategory: "Task management for AI-driven development"
---

Taskmaster (also written Task Master, and published on npm as `task-master-ai`) is a task-management
system for AI-driven development. Its README describes it as designed to work with any AI chat, and
in particular as built for development with Claude alongside [[SoftwareApplication/cursor]]; the
repository's description adds that it can be dropped into Cursor, Lovable, Windsurf, Roo and other
tools. It turns a project's requirements into a structured list of tasks that the developer's AI
assistant then plans against, breaks down and implements one at a time. Its documentation is published
on the website of Hamster, whose other products the README also links to.

## Capabilities

The workflow the README recommends starts from a product requirements document: "Always start with a
detailed PRD", on the stated reasoning that the more detailed the PRD, the better the generated tasks.
Taskmaster parses the PRD into tasks, and the developer then asks for the next task to work on, for
help implementing a particular task, or for a task to be expanded into subtasks; individual tasks can
also be created directly from a request in chat without a PRD. Tasks carry dependencies and can be
organised under tags, with commands to move tasks between tags with or without their dependencies. A
research command fetches fresh information, optionally with project context, and the documentation
also covers analysing task complexity, team collaboration and a loop command for automation.

Several of those commands call an LLM, so Taskmaster needs at least one provider configured. It
distinguishes three model roles — a main model, a research model, and a fallback model used when
either of the others fails — and supports Anthropic, OpenAI, Google Gemini, Perplexity (suggested for
research), xAI, OpenRouter and others through API keys, as well as [[SoftwareApplication/claude-code]]
and the Codex CLI ([[SoftwareApplication/openai-codex]]) through their own sign-in, with no API key
required.

There are two ways to run it. The recommended one is as a [[DefinedTerm/model-context-protocol]]
server configured in the editor — the README gives configuration paths for Cursor, Windsurf, VS Code
and Amazon Q Developer CLI, and a one-line install for Claude Code — after which the developer drives
it by talking to the editor's AI chat ("Initialize taskmaster-ai in my project", "What's the next task
I should work on?"). The other is the `task-master` command-line tool, with commands such as
`parse-prd`, `list`, `next`, `show` and `research`, and an `init` step that can also install rule files
for particular editors.

Because a large tool list costs context, the MCP server supports selective tool loading. By default
all 36 of its tools are loaded, which the README puts at roughly 21,000 tokens; a `standard` set of 15
tools and a `core` set of 7 (for example getting tasks, finding the next task, setting a task's status,
parsing a PRD and expanding a task) reduce that, and a custom comma-separated list is also accepted.
The README recommends the standard set for new users and the core set for large projects.

## Adoption & Ecosystem

Taskmaster is licensed under the MIT License with the Commons Clause. As the README summarises it,
the tool may be used for any purpose, modified and redistributed, and products built with it may be
sold, but Taskmaster itself may not be sold, offered as a hosted service, or used as the basis of a
competing product.
