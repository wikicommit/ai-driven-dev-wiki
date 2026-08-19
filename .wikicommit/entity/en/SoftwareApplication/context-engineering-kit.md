---
title: "Context Engineering Kit"
type: "schema:SoftwareApplication"
lang: en
tags: [context-engineering, agentic-coding, spec-driven-development, open-source]
sources:
  - type: url
    url: 'https://github.com/NeoLabHQ/context-engineering-kit'
    hash: sha256:bc2a9a7e51d46faa7b71b485a040ec8d6f6b10a78fc25f17a65dc7b9dde39b4c
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An open-source plugin marketplace of context engineering techniques for Claude Code and other coding agents, organised as granular plugins for reflection, spec-driven development, subagent orchestration, review, and structured reasoning."
  applicationCategory: "Agent plugin marketplace"
  author: "NeoLabHQ"
  operatingSystem: ""
  softwareVersion: "3.1.0"
  license: "GPL-3.0"
---

Context Engineering Kit (CEK) is an open-source collection of [[DefinedTerm/context-engineering]] techniques and patterns, distributed as a plugin marketplace for Claude Code, OpenCode, Cursor, Antigravity and other agents. Its stated aim is improving agent result quality and predictability with a minimal token footprint, and its maintainers describe it as based on prompts their company's developers used daily, supplemented by plugins derived from benchmarked papers and other projects.

The kit is deliberately granular: each plugin loads only its own agents, commands, and skills, so installing the marketplace alone adds nothing to context. Its skills follow the agentskills.io specification, and its spec-driven development plugin is built on the arc42 documentation standard adjusted for LLM capabilities.

## Overview

CEK's organising claim is a reliability-versus-cost trade-off. Its README presents a comparison table of approaches — a one-shot prompt, `/reflect`, `/reflect` plus `/memorize`, `/do-and-judge`, `/do-in-steps`, `/plan-task` plus `/implement-task`, adding `/brainstorm`, and adding human review — against the probability of a fully accurate result as the number of changed files grows, alongside each approach's token overhead. The stated pattern is that a one-shot prompt degrades sharply with scope (60–80% for 1–3 files down to 1–20% for 20+), while the heaviest pipeline with human review holds at 95–99% at 5×–35× the tokens. These figures are the maintainers' own, described as based on more than a year of real development usage on production projects rather than on a published benchmark.

Installation differs by host. Claude Code adds the marketplace and installs plugins individually; Gemini CLI and Antigravity CLI install every plugin's skills and agents as a single bundle, because neither supports per-plugin selection; and `npx skills` or OpenSkills can install the skills for Cursor, Codex, OpenCode and others, though the README notes that route does not carry subagents and so does not give the full experience.

## Features

The marketplace's plugins include:

- **Reflexion** — `/reflect`, `/memorize`, and `/critique`, plus a hook that runs `/reflect` automatically when the word appears in a prompt. The README grounds these in published work on self-refinement and reflection loops, and on agentic context engineering for memory updates after reflection.
- **Spec-Driven Development (SDD)** — the plugin the maintainers recommend starting with, alongside SADD. Three main commands (`/add-task`, `/plan-task`, `/implement-task`) drive a pipeline of specialised agents: `researcher`, `code-explorer`, `business-analyst`, `software-architect`, `tech-lead`, `developer`, `code-reviewer`, and `tech-writer`. See [[DefinedTerm/spec-driven-development]].
- **Subagent-Driven Development (SADD)** — commands for launching sub-agents, judging their output, and running work in parallel, in steps, or competitively. See [[DefinedTerm/subagent-driven-development]].
- **Review** — code and PR review using specialised agents (`bug-hunter`, `code-quality-reviewer`, `contracts-reviewer`, `historical-context-reviewer`, `security-auditor`, `test-coverage-reviewer`) with impact and confidence filtering, plus a triage command for narrowing a large changeset down for a human reviewer.
- **Test-Driven Development**, **Git**, **Domain-Driven Development**, **First Principles Framework (FPF)**, **Kaizen**, **Customaize Agent**, **Docs**, **Tech Stack**, and **MCP** — covering testing workflows, commit and PR creation, code quality rules, structured reasoning, root cause analysis, authoring commands and skills, documentation, language-specific rules, and MCP server setup.

Patterns the maintainers name as implemented in the Spec-Driven Development plugin include structured reasoning templates (chain of thought, tree of thoughts, problem decomposition, self-critique), multi-agent orchestration for context isolation to prevent context rot, quality gates based on [[DefinedTerm/llm-as-judge]], continuous learning that builds task-specific skills, and MAKER, a reliability pattern using clean-state agent launches and filesystem-based memory.

## History

The README's news section records the recent release line: v2.0.0 rewrote the SDD plugin from scratch; v2.1.0 and v3.1.0 progressively folded code quality guidance and a dedicated code-reviewer agent into it; v2.2.0 reworked SADD as a distilled version of SDD using meta-judge and judge sub-agents; and v3.0.0 added support for AMP and Hermes agents. The repository is licensed GPL-3.0 and, at the time of capture, showed 1.3k stars, 138 forks, and 395 commits.

On its relationship to [[DefinedTerm/vibe-coding]], the maintainers state that SDD is not a vibe coding solution but works like one out of the box: by default it runs from a single prompt to the end of a task, making evidence-based assumptions rather than repeatedly asking for clarification, on the reasoning that developer time is more valuable than model time. Their stated caveat is that quality will be sub-optimal without human feedback, and that they strongly advise decomposing work into smaller tasks and reviewing each specification independently.
