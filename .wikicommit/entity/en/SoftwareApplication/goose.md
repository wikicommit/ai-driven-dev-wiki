---
title: "goose"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-agents, open-source, cli, mcp]
sources:
  - type: url
    url: 'https://github.com/block/goose'
    hash: sha256:9e320d928a6bc22d89ce2015a058a7eb31b11dc5166a79f0f4a4f94290b68c9f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source, general-purpose AI agent that runs on the user's own machine as a desktop app, a CLI and an embeddable API, for coding as well as research, writing, automation and data analysis, and that connects to extensions through the Model Context Protocol."
  applicationCategory: "AI agent"
  operatingSystem: "macOS, Linux, Windows"
---

goose is an open-source AI agent, released under the Apache 2.0 license, that runs on the user's own
machine. Its README presents it as general-purpose rather than a coding tool alone — "for code,
workflows, and everything in between" — naming research, writing, automation and data analysis
alongside code as things to use it for, and the repository's description adds that it goes beyond
code suggestions to install, execute, edit and test with any LLM. The project is part of the Agentic
AI Foundation (AAIF) at the Linux Foundation, and its repository is published under the `aaif-goose`
organization on GitHub.

## Capabilities

goose comes in three forms: a native desktop app for macOS, Linux and Windows, a full CLI for terminal
workflows, and an API for embedding it elsewhere. It is written in Rust, which the README credits for
performance and portability.

It is model-agnostic. The README says it works with more than 15 providers, naming Anthropic, OpenAI,
Google, Ollama, OpenRouter, Azure and Bedrock among them, and that it can use either API keys or a
user's existing Claude, ChatGPT or Gemini subscription through ACP. Its capabilities are extended
through the [[DefinedTerm/model-context-protocol]]: the README states that it connects to more than 70
extensions via that open standard.

## Adoption & Ecosystem

Beyond the stock build, the project documents custom distributions — builds of goose with
preconfigured providers, extensions and branding — and publishes a governance document for the
project.
