---
title: "AI 代码审查再进化：AutoDev 多智能体协作架构深度解析"
type: "schema:BlogPosting"
lang: en
tags: [code-review, multi-agent, agent-architecture, coding-tools]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/autodev-multi-agents-code-review/'
    hash: sha256:652d5c90e9f8d8fae2da5a2576fa0fcaeb7b1469a256821bab8574f5912ceaa0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A November 2025 Chinese-language blog post by Phodal Huang describing the agentic code review in AutoDev: a four-step pipeline from static information collection to automated fixes, driven by a main CodeReviewAgent that orchestrates analysis sub-agents and a CodingAgent."
  author: ["Phodal Huang"]
  datePublished: "2025-11-26"
---

This post, written in Chinese by Phodal Huang, describes how code review is handled in
[[SoftwareApplication/unit-mesh-auto-dev]]. It opens with the pain points the author sees in code review in
real engineering environments: lint results, tests, issues and change records are scattered across different
systems, complex logic is hard to understand with any single tool, and manual review is slow and subject to
personal judgment. The post points readers to AutoDev CLI 0.3.0 (run as `autodev review -p .`) and to AutoDev
Desktop (compose-0.3.0) to try the feature.

Its central claim is that combining multi-agent collaboration with information aggregation lets AI understand a
change's context, history and quality risks the way a senior engineer would, and generate modification
suggestions or apply fixes directly, closing the loop from analysis to repair.

## Key Points

- The author describes the review flow as a four-step pipeline: static information collection (Code Audit),
  AI analysis (Code Analysis), modification plan generation (Modification Plan) and automated fixing (Generate
  Fixes).
- In the static collection step, changed hunks are extracted from the Git diff, tools such as CodeGraph locate
  the affected classes and methods, linters such as ESLint, Ktlint and Detekt are run, and related issues,
  requirements and tests are aggregated into structured data — a step the post says consumes no tokens.
- In the analysis step, the diff, structure, lint, issue and test data are built into a system prompt, analysed
  along different review types (comprehensive, performance, security, style), with tools such as `read_file` and
  `grep_search` used to fill in context where needed, producing structured findings with severity, location
  and suggestion.
- In the planning step, lint and AI findings are merged and prioritized into an executable fix plan that the
  user can add to or filter before it is used as input for the fix.
- In the fixing step, the CodeReviewAgent coordinates a CodingAgent that works from the actual changed hunks,
  making multiple rounds of tool calls (reading and writing files, refactoring, testing) and outputting a final
  patch that supports rollback and further iterations.
- The author's stated motivation for splitting the work across agents is that one agent struggles to keep
  stable throughput under token limits when review needs static analysis, context understanding, code
  generation and error recovery; separate agents can be combined as needed, evolve independently, and be
  degraded or replaced when analysis or a tool fails.
- The roles described are a main CodeReviewAgent that aggregates information, builds the prompt and decides
  which agent to call; analysis sub-agents — an AnalysisAgent for large content and complex context, an
  ErrorRecoveryAgent for tool-call and model-output errors, and a CodebaseInvestigatorAgent for repository-wide
  scanning — and a CodingAgent dedicated to code modification.
- Sub-agents are created and destroyed by a `SubAgentManager`, all tools including sub-agents are registered in
  a `ToolRegistry`, and execution, permissions and results are handled centrally by a `ToolOrchestrator`.

## Context

The post is a description of the author's own tool rather than an evaluation; it reports no measurements of
review quality. Its arrangement of a coordinating agent delegating focused tasks to sub-agents is an instance of
what this wiki describes as a [[DefinedTerm/sub-agent-architecture]]. The author says future work will
integrate test coverage, CI/CD and incremental analysis.
