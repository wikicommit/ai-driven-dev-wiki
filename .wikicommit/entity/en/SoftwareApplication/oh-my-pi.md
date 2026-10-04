---
title: "Oh My Pi"
type: "schema:SoftwareApplication"
lang: en
aliases: ["OMP"]
tags: [coding-agents, agent-harness, cli, open-source]
sources:
  - type: url
    url: 'https://habr.com/ru/companies/first/articles/1087842/'
    hash: sha256:14f534481b69f23e05689f880a735f18ca402a8de40aaa4197daab0d4f331dc3
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A fork of the Pi coding agent that builds in a broader set of development tools — LSP integration, a debugger, persistent Python and JavaScript sessions and task delegation — while keeping its harness open to modification."
  applicationCategory: "Coding agent"
  featureList: "LSP tools for diagnostics, navigation, renames and fixes; debugger via DAP; persistent Python and JavaScript sessions; task tool for delegation with workspace isolation; Agent Hub; Hashline line-and-hash editing; multi-provider model roles"
  url: "https://omp.sh/"
---

Oh My Pi (OMP) is a fork of [[SoftwareApplication/pi-coding-agent]] created by Can Bölük, described in [[BlogPosting/you-dont-need-another-claude-code-why-pi-leaves-agent-assembly-to-the-user]] as having a broader set of built-in development tools. It keeps Pi's split into components for working with models, executing the agent and the terminal interface, but makes more of the decisions about how they work together inside the project itself. The overview places it closer to [[SoftwareApplication/claude-code]], Codex CLI and [[SoftwareApplication/opencode]] — a ready tool for everyday coding — while noting that its harness source remains available to study and change, and that extensions can add tools and commands without maintaining one's own fork.

## Capabilities

OMP provides `LSP` tools for diagnostics, navigation, renames and applying the fixes a language server suggests, making these semantic operations part of the agent's normal work with code; the overview notes that results still depend on the language, the server and the project. It offers persistent Python and JavaScript sessions from which the agent's own tools can be called, with the JavaScript side using Bun, and a debugger connected through DAP giving the agent breakpoints, stepping, the stack and variables. For delegation it has its own task tool, including parallel work and optional workspace isolation, with an Agent Hub for observing and steering the workers. It supports multiple model providers and lets different models be assigned to different roles, such as one for main work and another for auxiliary tasks.

Its divergence from Pi goes beyond the tool list: a `pi-natives` package brings in native code through `N-API`, separate Rust components handle the shell, syntax trees, file traversal and workspace isolation, and an `omp-stats` component provides a local dashboard of model usage statistics. Its `Hashline` editing mechanism anchors edits to lines and hashes of their content, changing how the model specifies where to edit and how it gets feedback when the expected content does not match.

## Adoption & Ecosystem

The overview uses OMP to illustrate what it calls the pull of a fork: the more interconnected decisions of its own a fork accumulates, the more later changes must be reconciled with them, making it harder to maintain as a thin layer over the original.
