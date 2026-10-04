---
title: "Pi"
type: "schema:SoftwareApplication"
lang: en
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
  description: "A minimal terminal coding agent that builds its own harness from scratch and deliberately leaves features such as subagents, plan mode, task lists and permission prompts to extensions, so that it can serve as a programmable base for custom agents."
  applicationCategory: "Coding agent"
  featureList: "Terminal coding agent; extensions adding tools, commands, event handlers and UI elements; skills and prompt templates; packages; SDK embedding; RPC control"
  url: "https://pi.dev/"
---

Pi is a terminal coding agent that, according to [[BlogPosting/you-dont-need-another-claude-code-why-pi-leaves-agent-assembly-to-the-user]], builds its [[DefinedTerm/agent-harness]] from scratch rather than on top of an existing one. Its author, Mario Zechner, is described as having used [[SoftwareApplication/claude-code]] heavily in 2025 and being frustrated by how it was growing: features he did not need, and system instructions and tools that changed with updates, altering the model's behaviour and breaking familiar workflows, while making it hard to see what the agent was sending into the context. He wanted a tool with understandable sessions, access to its internals and the ability to build a different interface over the same agent, and published Pi in the `pi-mono` repository.

Pi's minimalism applies above all to this base: it is meant to be understandable and changeable enough that a user does not have to write an agent from scratch. It is nonetheless usable as-is, shipping with a terminal agent, basic tools and session management.

## Capabilities

From the start Pi was a set of components rather than only a terminal command: `pi-ai` provides a single interface to different language-model providers, `pi-agent-core` handles agent execution, tool calls and state, `pi-coding-agent` assembles these into a coding assistant, and `pi-tui` provides terminal interface components. An application can embed the ready agent through an SDK, control it from another process over RPC, or take `pi-agent-core` and define its own interface and rules.

Its standard distribution deliberately has no built-in subagents, plan mode, task list or permission prompts. These are left to extensions, third-party packages or separately launched agent instances; a plan can be kept in an ordinary file or given a dedicated mode. Extensions can add tools, commands, event handlers and interface elements, skills and prompt templates hold reusable instructions, and packages distribute all of these together. By default Pi runs with the permissions of the process that started it and has no built-in isolation of the file system, processes, network or credentials, so isolation requires a separately configured container or other restricted environment.

## Adoption & Ecosystem

[[SoftwareApplication/oh-my-pi]] is a fork that uses Pi as its base and builds in a wider set of development tools. The overview recommends Pi where control over the agent's design matters — an internal assistant, experiments with context, studying agent architecture or embedding the agent loop in a product.
