---
title: "Spec駆動開発におけるコンテキストエンジニアリングとCustom Slash Commandsのベストプラクティス"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, context-window, agent-config]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60229/'
    hash: sha256:10d03ac2a5d00b558656acc685e174052e16d06256b8fd88f86df9be1d954d01
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A CyberAgent tech lead's account, from a proof of concept still in progress, of context engineering in spec-driven development and of seven practices for designing custom slash commands."
  author: ["kajirita2002"]
  publisher: "[[Organization/cyberagent]]"
---

This post, written for day 13 of CyberAgent's 2025 developer Advent Calendar, is by a generative-AI and backend tech lead at [[Organization/cyberagent]] who is driving the renewal of an existing large-scale application on what the author calls a "spec-driven development platform". The author describes the effort as more than adopting an AI agent tool: it rebuilds existing systems and workflows so that code generation, specification writing, project management and operations are built and run on a prompt basis. At the time of writing the work was in its proof-of-concept phase.

The post places that work on CyberAgent's [[DefinedTerm/ai-maturity-levels]] for product-development teams, argues that reaching the top level (L4, "PRD to Production") requires a shift to [[DefinedTerm/spec-driven-development]], and names [[DefinedTerm/context-engineering]] as what decides whether that shift succeeds. Its main contribution is a set of design practices for [[DefinedTerm/custom-slash-commands]], drawn from the author's own proof of concept.

## Key Points

- The post defines spec-driven development as a method that redefines the specification not as a document for humans to read but as structured context from which AI generates code, so that documentation becomes the single source of truth from which code is produced.
- It argues the method's main benefit is a "healthy enforcement" on the process: because correct code cannot be generated without writing or updating the specification, documentation stays in step with the implementation, and fresh documentation lets newcomers ask an AI agent or RAG system about a feature's specification instead of reading it.
- It warns that the platform itself is hard to build, and that an immature one becomes new technical debt that forces inefficient processes on the development team.
- It defines context engineering as strategically designing and controlling the quality and quantity of the input information given to an LLM, and treats it as a means of diagnosing and fixing prompts whose output goes wrong.
- It names three context problems context engineering addresses: [[DefinedTerm/context-rot]], which the post describes as the premises an LLM holds growing stale over a long session and attributes mainly to too many input tokens burying early instructions; [[DefinedTerm/context-confusion]]; and [[DefinedTerm/context-poisoning]].
- It presents custom slash commands as the implementation means, with three benefits: standardized, reproducible prompt engineering; automated context injection, by having a command name the specification files to read; and version control of prompts as code in the repository.
- Single responsibility: an early command that chained web research, document creation, guideline checking and document correction was pulled off course by noisy search results, produced code that departed from the specification and skipped the guideline check. Splitting it into separate commands run in order (`create-reference`, `create-best-practices`, `create-design-doc`, `review-architecture`) improved output quality and made faulty instructions easier to locate — the author's own PoC experience.
- Minimize context: loading unneeded documents, such as an unrelated agents file or a whole large codebase, lowers the signal-to-noise ratio, buries important instructions and raises cost and latency; the post recommends injecting only the minimum necessary information.
- Predefine outputs and templates: the post likens a command to a function (input context and prompt, logic, output artifact), asks that the output's structure be defined first, and uses templates to force the output's format. It states a paradox that the smarter a model is, the more its format drifts when given freedom.
- Make commands testable: in a domain-free sandbox such as a to-do app, a human first writes the ideal output as golden data, then the command is tuned until its output matches — a golden-master approach the post proposes for quality-controlling commands.
- One artifact per command: every command, including review and research commands, should persist its result as a Markdown file rather than leave it in the console. Files become the interface between commands, which lets a read-heavy review step and a write step be separated by clearing the context in between; the post notes that splitting too finely raises the cognitive cost of managing command order.
- Avoid tool dependence: tool-specific features and tool names should stay out of prompts, and core command logic should live under `docs/`, with tool-specific settings acting only as thin wrappers that reference it. The author did not adopt Claude Code's SubAgents, reporting that in the PoC delegation cost more to control than ordinary commands and gave unstable quality, and concludes that feeling the need for a SubAgent is a sign the task is too complex.
- Simple instructions: long explanations or if-else branching inside a prompt are treated as a signal that a command has taken on too much and should be split.
- The author advises introducing spec-driven development first within a scope one controls — one's own tasks or a small team — and widening it gradually, because defining workflows and artifacts is hardest in mature organizations with many stakeholders.

## Context

All of the practices are the author's own findings from a proof of concept still under way inside one company, not measured results or an established convention, and the post says so in framing them as knowledge gained through the PoC. The four-level maturity model it opens with is presented as CyberAgent's own internal definition.
