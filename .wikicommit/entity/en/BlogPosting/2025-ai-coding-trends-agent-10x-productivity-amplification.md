---
title: "2025 年 AI 编程趋势：智能体 10 倍生产率放大下的“粪围”蔓延"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, ai-assisted-programming, technical-debt, vibe-coding, mcp]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/2025-ai4se-coding-trends/'
    hash: sha256:184c9312b84e3b9dedfc953ffdc58b2dde10880b874e1d8b2a7a1b10f60187c8
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A July 2025 Chinese-language blog post by Phodal Huang surveying AI coding trends in 2025 — agent proliferation, plan-first workflows, automated verification, asynchronous agents, SDLC-wide tooling and MCP — and arguing that coding agents amplify existing practice rather than simply speeding it up, so that code produced without deliberate architecture accumulates technical debt."
  author: ["Phodal Huang"]
  datePublished: "2025-07-04"
---

Written in Chinese by Phodal Huang, whose author profile on the site describes him as a Thoughtworks
technical expert, this post takes stock of AI coding in mid-2025. It opens by saying that 2025 is not
merely a "year of the agent" but the starting point of a systemic leap, and names three signs: Cursor and
Windsurf moving from AI editors to AI IDEs, Claude Code reshaping task execution around the model's
reasoning ability, and Augment's closed-loop verification. Its thesis is stated in bold: what agents
bring is not simple efficiency but amplification — what was done badly before is now done worse.

The body walks through eight trends and closes with a summary whose main warning is that the
"10x productivity" agents promise is real but comes with high, compounding "hidden interest" in the
form of technical debt, which, left unchecked, will eventually crush an engineering organisation.

## Key Points

- The author reports using code completion much less over the preceding half year because agents can
  understand requirements and carry out whole sequences of development tasks. He argues that top models
  are now a general "intelligence engine" every tool vendor can plug into, so competition has moved to
  workflow, user experience and ecosystem integration.
- He describes a shift from generating code directly to "plan first, code later": planning in a
  Markdown roadmap, writing a detailed self-contained prompt per task, handing the AI one task at a time,
  and reviewing each result before moving on. He cites [[SoftwareApplication/claude-code]]'s
  `TodoRead`/`TodoWrite` tools and [[SoftwareApplication/windsurf]]'s `update_plan` as examples of tools
  updating a task list as they work.
- Automated verification has strengthened, in his account especially in Claude and Augment: not just
  unit tests but human-like checking — trying several verification approaches, multiple rounds of
  testing, and writing lighter throwaway test scripts to rule out unrelated errors.
- AI coding is moving from foreground interaction to asynchronous background execution, with Augment
  Remote Agent and Cursor Backend Agent as examples; he names remote development infrastructure,
  context engines and the [[DefinedTerm/model-context-protocol]] as its three supporting pillars.
- He argues that building organisation-level MCP capability is essential once agents are adopted, and
  notes that because the protocol lacked authentication at the time, enterprises had to solve that
  themselves.
- On architecture, he reports that prototypes he built with Augment and Cursor produced tightly coupled,
  hard-to-maintain code when generated from a vague idea without an architectural plan, and argues that
  AI-assisted refactoring is unreliable because the AI may treat an intended architectural change as an
  error and "fix" it back.
- He cites third-party research on AI-assisted code quality as showing a sharp rise in duplicated code
  during 2024, and says his own experience with agents suggests the effect could be larger still. He
  attributes to Thoughtworks colleagues the warning that AI amplifies indiscriminately: if you are
  making mistakes, it helps you make them faster and at larger scale.
- He presents [[DefinedTerm/vibe-coding]] as where this amplification shows most clearly, especially for
  less experienced developers relying on fast AI responses without planning.

## Context

The post is a practitioner's opinion piece rather than a study; apart from the duplication research it
cites, its evidence is the author's own use of the tools. To frame the verification trend it reuses three
characteristics the author had earlier proposed for "AI coding tools 2.0" — agent-driven,
developer-experience-first and automated verification. It also lists many tools by SDLC stage
(research, prototyping, requirements, code generation, code quality, testing, operations) and
integrated offerings such as [[SoftwareApplication/github-copilot]] and Atlassian Rovo, without
evaluating them.
