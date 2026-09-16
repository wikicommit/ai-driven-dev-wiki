---
title: "Agent Skills"
type: "schema:SoftwareApplication"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agent-skills/'
    hash: sha256:b9423cb1290bb467c3a66aa51884a5717037c14bd668eeca8b09ca3fba6fa781
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An MIT-licensed, open-source library of twenty markdown-based skills and seven slash commands for AI coding agents, organized around six SDLC phases, meant to enforce senior-engineer practices (specs, tests, review, scope discipline) that agents otherwise skip."
  applicationCategory: "AI coding agent skill library"
  featureList: "/spec, /plan, /build, /test, /review, /ship, /code-simplify slash commands; twenty markdown skills with anti-rationalization tables and progressive disclosure"
  author: "Addy Osmani"
---

Agent Skills is an open-source, MIT-licensed library of twenty markdown-based skills for AI coding agents, published by its author on GitHub, reported to have crossed 27,000 stars. Each skill is a workflow file with checkpoints and a defined exit criterion, rather than reference documentation, meant to bolt senior-engineer discipline (writing a spec, writing tests first, sizing a change for review) back onto an agent that would otherwise take the shortest path to a finished-looking diff.

## Capabilities

The library organizes its twenty skills around six SDLC phases — define, plan, build, verify, review, ship — surfaced through seven slash commands: `/spec`, `/plan`, `/build`, `/test`, `/review`, `/ship`, and `/code-simplify`. A router skill, `using-agent-skills`, decides which of the twenty skills apply to a given task, so a small bug fix activates only a few while a complex feature can activate around eleven in sequence. Each skill embeds [[DefinedTerm/anti-rationalization-tables]] pairing common excuses for skipping the workflow with a written rebuttal, and skills are loaded via progressive disclosure rather than all at once.

Three ways of using it are described: installing it as a Claude Code plugin (`/plugin marketplace add addyosmani/agent-skills`, then `/plugin install agent-skills@addy-agent-skills`), dropping the plain markdown files into another tool's own system-prompt mechanism (e.g. Cursor's `.cursor/rules/`, Gemini CLI, Codex, Aider, Windsurf, OpenCode), or reading the skill files themselves as a specification of practice without installing anything.

## Adoption & Ecosystem

The skills are described as saturated with practices drawn from *Software Engineering at Google* and Google's public engineering culture, including Hyrum's Law, the test pyramid and Beyoncé Rule, DAMP-over-DRY testing, ~100-line PR sizing with Critical/Nit/Optional/FYI severity labels, Chesterton's Fence, trunk-based development, shift-left CI/CD, and treating code as a liability in deprecation decisions. The project is presented as one layer of the author's broader [[DefinedTerm/harness-engineering]] framing, sitting alongside `AGENTS.md`, hooks, and tools.
