---
title: "构建演进式 AI 辅助编码，融合 DevOps 规范和实践"
type: "schema:BlogPosting"
lang: en
tags: [ai-assisted-programming, coding-tools, software-process]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/build-devops-inside-practise-for-ai-coding/'
    hash: sha256:e4e7bc07f479e47a0e678208bbfb58443125067f5e88b81a88b42c3f55c54f38
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An April 2024 Chinese-language blog post by Phodal Huang arguing that assisting code changes, rather than regenerating code, is the practical path for AI coding, and describing features of AutoDev 1.8 that build DevOps conventions into the tool: requirement-linked commit messages, code-smell-driven refactoring, AI rename suggestions and terminal command generation."
  author: ["Phodal Huang"]
  datePublished: "2024-04-06"
---

This post, written in Chinese by Phodal Huang, introduces a new version of
[[SoftwareApplication/unit-mesh-auto-dev]] that builds a series of software development practices into the
tool: AI renaming, code-smell refactoring and refactoring suggestions, commit message generation, CLI command
generation, and — which he singles out as most important — Chinese prompt support, to suit domestic models and
development habits.

Its framing argument is that generative AI coding has two technical routes: regenerating code or changing code.
The author describes Unit Mesh as an architectural paradigm his team designed for the regeneration route, in which
new code is generated for each new requirement, and argues that however good regeneration gets it is limited by
generative AI's abilities, so a code-change assistant such as AutoDev is the suitable evolutionary path for now.
Assisting changes requires humans and AI to understand the existing code, which, he argues, depends on having
built a knowledge-engineering system for software development.

## Key Points

- The author names two typical scenarios for this knowledge engineering: summarizing how an existing requirement
  is implemented, and refactoring, which he calls a good area for exploration because its difficulty lies between
  generating code automatically and designing architecture.
- He argues that retrieval-augmented generation can supply extra information but does not suit developers'
  everyday, high-frequency scenarios, so the challenge is to build conventions, best practices and software
  knowledge engineering into the AI assistance tool itself to raise the baseline.
- On refactoring, he argues that AI refactoring depends on context and intent: without a clear direction AI mostly
  applies basic techniques such as renaming and extracting methods, whereas telling it to move multiple `if`
  statements to a strategy pattern, or giving it the inheritance relationships or the code smells, makes it take
  those into account.
- He describes two scenarios that block AI from linking code to requirements when development is not
  sufficiently digitized: requirements that were never recorded in detail, leaving the code as the only record,
  and code full of identifiers that even humans cannot understand.
- Commit message generation is presented as automating a DevOps convention: the IDE connects to the internal OA
  system for the user's identity, retrieves the user's current requirement ID, and combines it with the code
  change to generate a message such as
  `refactor(rename): handle exceptions and improve logging for rename suggestions #129`, which the author calls a
  foundation for a "digital twin" of development.
- Code-smell refactoring takes results from the IDE's own code inspection — for example that a variable is never
  used — and turns them into input the AI can use to produce refactored code or refactoring suggestions; the
  author says AutoDev 1.8 optimized its prompts by copying JetBrains' and also offers random refactoring
  suggestions.
- Semantic renaming generates five name suggestions for a function or class when the user invokes the IDE's
  rename feature, so that renamed code entities stay searchable; because renaming is frequent, it must be enabled
  manually in the settings.
- Terminal CLI generation puts the date, operating system and shell into the context, so that asking to "create
  today's branch" yields a command such as `git checkout -b feature/20240406`, and organizations can add further
  conventions of their own.

## Context

The post doubles as release notes for AutoDev 1.8, whose other listed changes include a Chinese settings page and
prompts, an easier way to test the LLM server from the settings page, support for 2024.1 IDE versions,
improvements to AutoSQL error handling, and line-and-column code references. The author closes by naming the
tool's own challenge: with so many features, developers unfamiliar with the plugin find it hard to get started.
