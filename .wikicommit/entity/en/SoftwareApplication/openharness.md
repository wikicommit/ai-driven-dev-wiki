---
title: "OpenHarness"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-tooling, agent-architecture, open-source]
sources:
  - type: url
    url: 'https://github.com/HKUDS/OpenHarness'
    hash: sha256:9bbda0914ba868f48d4405712010871672d985e50cc184e63fbbbd2d0a88071e
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source Python agent harness from HKUDS that provides lightweight agent infrastructure — an agent loop, tools, skills, plugins, permissions, hooks, memory and multi-agent coordination — through the `oh` command-line tool, and that is designed to stay compatible with Claude-style skills and plugins."
  applicationCategory: "Agent harness"
  author: "HKUDS"
---

OpenHarness is an open-source Python implementation of an [[DefinedTerm/agent-harness]], published by HKUDS under the MIT license and launched with a single command, `oh`. Its README defines an agent harness as the complete infrastructure that wraps around an LLM to make it a functional agent — the model provides intelligence, while the harness provides "hands, eyes, memory, and safety boundaries" — and closes on the line "The model is the agent. The code is the harness."

The project describes itself as a community-driven research project aimed at researchers and builders who want to understand how production AI agents work under the hood, experiment with tools, skills and agent coordination patterns, extend the harness with their own plugins and providers, and build specialized agents on top of it. The same repository ships [[SoftwareApplication/ohmo]], a personal agent built on OpenHarness.

## Capabilities

At its centre is an agent loop: the harness streams a model response, and for as long as the model asks for tools it runs each tool call through a permission check and lifecycle hooks, appends the results to the conversation and loops again, stopping when the model is done. In the README's words, the model decides what to do and the harness handles how. Around that loop the project lists subsystems for tools (43 or more, spanning file operations and shell, web and code search, notebook editing, subagents and teams, background tasks, MCP, plan-mode and worktree switching, and scheduled or remote execution), on-demand skills loaded from `SKILL.md` directories, plugins that bundle commands, hooks and agents, permissions, PreToolUse and PostToolUse [[DefinedTerm/agent-hooks]], slash commands, an MCP client, persistent memory, background tasks and multi-agent coordination. Context handling covers discovering and injecting CLAUDE.md files, automatic context [[DefinedTerm/compaction]], a MEMORY.md persistent memory file and session resume.

Permissions come in three modes — a default mode that asks before writing or executing, an auto mode that allows everything and is meant for sandboxed environments, and a plan mode that blocks all writes — plus path-level rules and denied commands set in a settings file. The `oh` tool runs interactively in a React/Ink terminal interface, or non-interactively with text, JSON or streaming-JSON output for scripts. A dry-run mode resolves settings, authentication, prompt assembly, skills, commands, tools and MCP configuration without calling the model, executing tools, spawning subagents or connecting to MCP servers, and reports a ready, warning or blocked verdict with suggested next actions. Model providers are configured as named workflow profiles covering Anthropic-compatible and OpenAI-compatible APIs, Claude and Codex subscriptions, and GitHub Copilot, which also admits local models served through Ollama's OpenAI-compatible endpoint.

## Adoption & Ecosystem

OpenHarness states compatibility with the `SKILL.md` directory layout of Anthropic's skills repository ([[DefinedTerm/agent-skills]]) and with [[SoftwareApplication/claude-code]] plugins, reporting that it was tested with 12 official plugins, and it also discovers skills from `.claude/skills` and `.agents/skills` directories. Its README positions it as a lightweight harness layer around Claude-style tooling conventions, suited to [[SoftwareApplication/openclaw]]-oriented workflows and to multi-agent work in the style of ClawTeam, and suggests uses as a repository coding assistant, a headless scripting tool, a testbed for skills and plugins, a multi-agent prototype harness and a sandbox for comparing providers. The initial open-source release was dated 1 April 2026.
