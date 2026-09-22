---
title: "Mistral Vibe CLI"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, coding-tools, cli, open-source]
sources:
  - type: url
    url: 'https://mistral.ai/news/devstral-2-vibe-cli'
    hash: sha256:2138589678ecaf64d2613d8944af216e4e3b69049df0e348b80da6cd73da9788
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source command-line coding assistant from Mistral AI, built for the Devstral models, that explores, modifies and executes changes across a codebase from natural-language instructions in the terminal or inside an IDE. Released under the Apache 2.0 license."
  applicationCategory: "Command-line coding agent"
  featureList: "Project-aware context assembled from file structure and Git status; @ autocomplete for file references; ! for shell command execution; slash commands for configuration; multi-file orchestration; persistent history and autocompletion; customizable themes; programmatic invocation for scripting; auto-approval toggle for tool execution; local model and provider configuration through config.toml; tool permission control"
  author: "Mistral AI"
---

Mistral Vibe CLI is a command-line coding assistant published by Mistral AI and released under the
Apache 2.0 license. It is built for the Devstral model family and was announced alongside Devstral 2
in [[BlogPosting/introducing-devstral-2-and-mistral-vibe-cli]]. It works from natural-language
instructions, exploring a codebase, modifying it and executing the resulting changes, and it runs
either in the terminal or inside an IDE.

It belongs to the category of terminal-resident [[DefinedTerm/ai-coding-agent]] tooling, and what
distinguishes it in Mistral's own framing is that both the agent and the models it is designed
around are openly licensed — the agent under Apache 2.0, and Devstral Small 2 likewise, with
Devstral 2 under a modified MIT license. Mistral presents the pair as an end-to-end open
alternative for [[DefinedTerm/agentic-coding]] work that would otherwise depend on a hosted,
proprietary model.

## Capabilities

The CLI presents an interactive chat interface backed by tools for file manipulation, code
searching, version control and command execution. Mistral describes it as project-aware: it scans
the file structure and Git status on its own to assemble context, rather than requiring the user to
name the relevant files. Within a session, files can be referenced with `@` autocomplete, shell
commands run with `!`, and configuration changed through slash commands. Sessions carry persistent
history and autocompletion, and the interface supports customizable themes.

Mistral states that the CLI reasons over the whole codebase rather than only the open file, which
it calls multi-file orchestration and describes as enabling architecture-level reasoning. The claim
that this can halve PR cycle time is Mistral's own, made in the launch announcement without
supporting measurement.

The CLI can be invoked programmatically for scripting. Tool execution can be set to auto-approve
or left gated, tool permissions can be restricted, and local models and providers are configured
through a `config.toml` file. For use with Devstral, Mistral recommends a temperature of 0.2.

## Adoption & Ecosystem

Mistral Vibe CLI integrates with an IDE through the Agent Communication Protocol, and is
distributed as an extension for the Zed editor so that it can be driven from inside that editor
rather than a separate terminal.

The announcement positions the CLI as the native harness for Devstral, but the models are also
distributed to third-party agent tooling: Mistral names Kilo Code and Cline as partners it worked
with to make Devstral 2 available in tools developers already use. The CLI is therefore one of
several ways to run these models agentically rather than the only one, and Mistral publishes best
practices for it in the project's own repository README.
