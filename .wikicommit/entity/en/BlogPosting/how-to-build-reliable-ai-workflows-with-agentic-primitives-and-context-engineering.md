---
title: "How to build reliable AI workflows with agentic primitives and context engineering"
type: "schema:BlogPosting"
lang: en
tags: [agent-primitives, context-engineering, prompt-engineering, markdown, tooling]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/how-to-build-reliable-ai-workflows-with-agentic-primitives-and-context-engineering/'
    hash: sha256:f4175892bf17116173c4ae2a309b3b81b227800f09d53afa3ad1ade536e02a2d
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A guide on GitHub's blog proposing a three-layer framework — Markdown prompt engineering, agent primitives, and context engineering — for turning ad-hoc AI experimentation into a repeatable engineering practice, and arguing that the resulting Markdown files are software that needs runtime, packaging and deployment infrastructure of its own."
  author: "Daniel Meppiel"
  datePublished: "2025-10-13"
  publisher: "[[Organization/github]]"
---

This guide argues that starting from a prompt works for simple fixes but breaks down as work gets
more complex or more collaborative, and proposes a three-part framework in its place. The two
concepts at its core are [[DefinedTerm/agent-primitives]] — reusable, configurable building blocks
that let AI agents work systematically — and [[DefinedTerm/context-engineering]], which it defines
as ensuring agents always focus on the right information. The stated goal is AI systems that code
independently while doing so reliably, predictably and consistently.

The framework's three layers are presented as building on one another. Layer 1 is Markdown as a
vehicle for prompt engineering: its headers, lists and links are said to guide the model's
reasoning and make outputs more predictable. Layer 2 turns those techniques into files —
`.instructions.md`, `.chatmode.md`, `.prompt.md`, `.spec.md`, `.memory.md`, `.context.md` — each
carrying a specific capability or rule. Layer 3 is context engineering, addressing what the post
frames as the remaining failure mode: even good prompts and primitives fail when faced with
irrelevant context competing for limited model attention.

The second half of the post makes a different kind of argument. It holds that these Markdown files
are genuine software written in natural language rather than code — modular, reusable, with
dependencies, evolution and distribution — and that they therefore need the same infrastructure
any other software ecosystem developed: runtimes, a package manager, and CI/CD deployment. The
post's answer to that need is [[SoftwareApplication/apm-agent-package-manager]], which the author
also maintains.

## Key Points

- The framework is summarized as Markdown prompt engineering plus agent primitives plus context
  engineering equals reliability.
- A core agent primitive is defined as a simple, reusable file or module providing a specific
  capability or rule for an agent.
- Markdown links in a prompt are framed as context injection points that pull in relevant
  information, either from files or websites.
- Chat modes are presented as professional boundaries analogous to real-world licensing: the post's
  framing is that professional licenses keep architects from building and engineers from planning,
  and its illustration is that you would want an architect to plan a bridge and not build it. Each
  mode is given only the MCP tools its domain needs, which the post frames as preventing
  cross-domain security breaches.
- Context engineering techniques the post names are session splitting (separate agent sessions for
  planning, implementation and testing), targeted `.instructions.md` files scoped with an `applyTo`
  YAML frontmatter pattern, memory-driven development via `.memory.md`, context helper files, and
  chat modes used to keep the model's attention on one domain.
- Agentic workflows are defined as `.prompt.md` files that coordinate multiple primitives into
  complete processes, designed to run in an IDE, in a terminal, or in a CI pipeline.
- The post distinguishes an inner loop — interactive development, testing and refinement in VS Code
  with GitHub Copilot — from an outer loop of agent CLI runtimes handling reproducible execution,
  CI/CD integration and production deployment. See [[DefinedTerm/outer-loop]], where this wiki
  records a different sense of the same pair of terms.
- It claims that VS Code natively supports `.instructions.md`, `.prompt.md` and `.chatmode.md`,
  while `.spec.md`, `.memory.md` and `.context.md` are patterns this framework adds on top.
- The ecosystem evolution it predicts runs in four stages: raw code as agent primitive files,
  runtime environments as agent CLI runtimes, package management, and a thriving ecosystem of
  shared libraries and community packages — explicitly modelled on npm's role in JavaScript's
  growth.
- The post recommends starting in a fixed order: instructions first, then chat modes, then reusable
  prompts, then specification templates.
- Its stated outcome for the practice is compound intelligence — capturing implementation failures
  in `.memory.md`, documented patterns in `.instructions.md`, and refined workflows in `.prompt.md`
  — that improves through iterative refinement. This is the author's framing of the benefit rather
  than a measured result; the post reports no evaluation of the framework.

## Context

The post is published on GitHub's own blog and its worked examples run on GitHub products
throughout — GitHub Copilot in VS Code for the inner loop, GitHub Copilot CLI recommended as the
agent CLI runtime for the outer loop, `copilot-instructions.md` in a `.github` folder, the GitHub
MCP server as a declared dependency, GitHub Actions for production deployment, and GitHub's own
`spec-kit` recommended for building specification templates. The package-management layer is the
exception, and it is the layer the second half of the argument turns on: APM, and the
`awesome-ai-native` documentation the post links to throughout, are the author's own projects
rather than GitHub's. That is the relationship to keep in view when reading the claim that agent
primitives need a package manager.

Where the post's file conventions are vendor-specific, it says so: it distinguishes the three file
types VS Code supports natively from the three its framework introduces, and it notes that GitHub
offers custom instructions for repository-specific guidance. The claim that the ecosystem will
follow the same path as previous programming ecosystems is offered as a pattern the author reads
from that history, not as evidence.
