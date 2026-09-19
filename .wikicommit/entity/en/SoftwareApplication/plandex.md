---
title: "Plandex"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, cli, context-engineering, human-oversight]
sources:
  - type: url
    url: 'https://github.com/plandex-ai/plandex'
    hash: sha256:a738983d749d3b45d039c45d6973d1692a45b01f1f77806838a84b063fe0c1cc
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source, terminal-based AI coding agent that plans and executes coding tasks spanning many steps and dozens of files, keeping its changes in a cumulative diff review sandbox until they are applied. It ships as a CLI plus a server that can be self-hosted with Docker, and is published under the MIT license."
  applicationCategory: "AI coding agent"
  operatingSystem: "Terminal/CLI; on Windows, only inside WSL"
  featureList: "Cumulative diff review sandbox; tree-sitter project maps and syntax validation across 30+ languages; configurable autonomy from full auto to step-by-step review; automated debugging of terminal commands and, with Chrome installed, browser applications; project-aware chat mode; curated multi-provider model packs; plan-level version control with branches; git integration; REPL and scriptable CLI"
  author: "[[Organization/plandex-ai]]"
---

Plandex is an open-source [[DefinedTerm/ai-coding-agent]] that runs in the terminal. The project
describes it as a development tool that can plan and execute large coding tasks spanning many steps
and touching dozens of files, and states that it is designed for large projects and real-world
tasks. Its README positions it against tools it says struggle once a project grows past a certain
size or the changes become too complex.

It is distributed as a one-line, zero-dependency CLI install together with a server that can be run
locally in Docker or hosted on the user's own machine. The CLI is invoked as `plandex`, with `pdx`
as a short form, and the repository is published under the MIT license. Windows is supported only
through WSL — the project states Plandex does not work correctly in the Windows command prompt or
PowerShell.

## Capabilities

Context handling is the capability the project puts first. It states an effective context window of
2M tokens with the default model pack — roughly 100k per file — and says Plandex loads only what
each step needs. Directories of 20M tokens or more are indexed using tree-sitter project maps, which
the project also uses for syntax validation and says covers more than 30 languages. Context caching
is used for OpenAI, Anthropic and Google models, which the project says reduces cost and latency.

Changes are staged rather than written straight into the project. The README calls this a cumulative
diff review sandbox: AI-generated changes are kept separate from the project's files until they are
ready to apply, and command execution is controlled so that a run can be rolled back and debugged.
The project presents this as the mechanism that keeps an agent from leaving a mess behind in a
codebase.

Autonomy is configurable rather than fixed. The project states Plandex is capable of full
autonomy — loading relevant files, planning and implementing changes, executing commands and
debugging automatically — while also offering fine-grained control and a step-by-step review process
where that is wanted. Automated debugging covers terminal commands such as builds, linters, tests,
deployments and scripts, and, where Chrome is installed, browser applications as well.

Alongside implementation there is a project-aware chat mode, which the project describes as a way to
flesh out ideas before moving to implementation and to ask questions about a codebase. Models from
several providers can be combined, with curated model packs offered as different tradeoffs of
capability, cost and speed, including open-source and provider-specific packs. The project describes
its file edits as prioritising correctness, validating both syntax and logic as needed with multiple
fallback layers when problems arise.

Every update to a plan is placed under version control of its own, including branches for exploring
multiple paths or comparing different models. This sits alongside git integration with commit
message generation and optional automatic commits. The developer-facing surface is a REPL with fuzzy
auto-complete for commands and file loading, plus a CLI for scripting or piping data into context.

## Adoption & Ecosystem

Plandex is run against a model provider the user supplies. The project documents an OpenRouter.ai
key as one option and points at other model provider accounts and API keys as alternatives, and
states that a Claude Pro or Max subscription can be connected for calls to Anthropic models, with
the prompt to connect one appearing on first run.

Of the two hosting options the README lists, the managed one is being retired: it states that
Plandex Cloud is winding down as of 10/3/2025 and is no longer accepting new users. Self-hosted and
local mode — Docker locally, or the server on the user's own infrastructure — is the remaining
route.

The project is developed in the open on GitHub, with a Discord server, GitHub Discussions and an
issue tracker named as the places for feedback and questions, and documentation hosted separately at
docs.plandex.ai.
