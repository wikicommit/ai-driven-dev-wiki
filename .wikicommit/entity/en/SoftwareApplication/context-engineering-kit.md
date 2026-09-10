---
title: "Context Engineering Kit"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, llm, prompting]
sources:
  - type: url
    url: https://github.com/NeoLabHQ/context-engineering-kit
    hash: sha256:3a00d5fa6029f48343ba32101feda4acd0f31870b7ff74ef954be99d4e04a584
    license: GPL-3.0
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "A marketplace of context-engineering plugins for AI coding agents, packaging prompt patterns as installable skills, commands and sub-agents for Claude Code, Gemini CLI, Antigravity, Cursor and other tools."
  applicationCategory: "Plugin marketplace for AI coding agents"
  featureList: "Per-plugin installation with no dependencies; command-oriented skills backed by sub-agents; thirteen plugins spanning reflection, specification-driven and subagent-driven development, review, testing, Git, documentation and MCP setup; a hook that triggers reflection from the word \"reflect\" in a prompt; GitHub Actions integration for code review"
  author: "[[Organization/neolabhq]]"
---

Context Engineering Kit is a marketplace of [[DefinedTerm/context-engineering]] plugins for AI
coding agents, published by [[Organization/neolabhq]] and distributed from a public GitHub
repository under the GPL-3.0 licence. It describes itself as a hand-crafted collection of advanced
context engineering techniques and patterns with a minimal token footprint, aimed at improving the
quality and predictability of an agent's results, and it targets [[SoftwareApplication/claude-code]],
OpenCode, [[SoftwareApplication/cursor]], Antigravity and other agents.

The kit's contents come from two places. The project says the marketplace is based on prompts its
own developers have used daily over a long period, supplemented by plugins derived from benchmarked
papers and from other projects it judges to be high quality. It publishes a separate list of the research
behind that second group, covering refinement loops, memory integration and curation,
principle-based critique, evaluation patterns, multi-agent debate, structured exploration,
step-by-step reasoning and verification, and hallucination reduction.

What is distributed is prompt material rather than executable software: skills, slash commands,
rules and sub-agent definitions that an agent loads into its own context. The project states that
its skills follow the [agentskills.io](https://agentskills.io) specification, and that the
specification template used by its Spec-Driven Development plugin is based on the arc42
documentation standard, adjusted for what an LLM can work with.

## Capabilities
The kit is installed as a marketplace rather than as a single bundle, and the project treats that
granularity as one of its design goals — each plugin loads only its own agents, commands and
skills, so a user installs just the ones they need. In Claude Code the marketplace is added with
`/plugin marketplace add NeoLabHQ/context-engineering-kit`, which makes the plugins available
without loading anything into context, and each plugin is then installed individually, for example
`/plugin install reflexion@NeoLabHQ/context-engineering-kit`.

Other agents are supported with less granularity, which the project states plainly rather than
glossing over:

- **Gemini CLI** installs the repository as an extension, and **Antigravity CLI** installs from the
  repository's `antigravity/` folder. Both take every plugin's skills and agents as a single bundle;
  the project notes that neither CLI supports per-plugin selection, and suggests deleting the
  unwanted skills after installation.
- **Cursor, Codex, OpenCode and others** install through `npx skills add`, where individual skills
  can be picked. Because each of those providers uses its own agent format and that installer does
  not support sub-agents, the project says this route does not give the full experience.
- OpenSkills is offered as a further alternative.

The plugins themselves fall into a few groups. Reflexion supplies `/reflect`, `/memorize` and
`/critique` for feedback and refinement loops, together with a hook that runs `/reflect`
automatically when the word "reflect" appears in a prompt — the hook requires `bun`, though the
commands themselves do not. Spec-Driven Development and Subagent-Driven Development implement the
methodologies described in [[DefinedTerm/spec-driven-development]] and
[[DefinedTerm/subagent-driven-development]]. Review provides code and pull-request review through
six specialised agents — bug-hunter, code-quality-reviewer, contracts-reviewer,
historical-context-reviewer, security-auditor and test-coverage-reviewer — with impact and
confidence filtering, and the project positions it as an open-source alternative to CodeRabbit that
can also run in GitHub Actions. The remainder cover Git operations, test-driven development,
Domain-Driven Development rules for Clean Architecture and SOLID, the
[[DefinedTerm/first-principles-framework]], Kaizen-style root-cause analysis, authoring of an
agent's own commands and skills, documentation, language-specific rules, and setup of Model Context
Protocol servers.

## Adoption & Ecosystem
The project publishes a comparison of how much scaffolding an agent is given against how reliably it
produces fully accurate results, running from a bare one-shot prompt through reflection, judge
sub-agents and per-file-group execution up to a written specification with human review. Its shape
is the argument: reliability rises along that progression while token overhead rises with it, from
none for a one-shot prompt to a multiple of the baseline for the specification-driven route, and the
gap widens as the number of changed files grows. The figures are the project's own, described as
based on more than a year of real development usage on production projects rather than on an
independent benchmark, and the accompanying claims for the Spec-Driven Development plugin — that it
produced working code in every case its team tested — are self-reported in the same way.

The project frames its three reliability-oriented plugins as complementary rather than competing,
the choice between them being a trade of reliability against token cost, and recommends starting
with Subagent-Driven Development and Spec-Driven Development. Two of its other projects are
presented as companions: Agent Sandbox, a development sandbox image for agents based on Microsoft's
official devcontainers images, and Agent Eslint Config, an ESLint configuration intended to push
agents toward low-complexity, readable code. Both are said to work independently of the kit.
