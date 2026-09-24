---
title: "Codified Context: Infrastructure for AI Agents in a Complex Codebase"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, context-engineering, experience-report, multi-agent]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.20478'
    hash: sha256:7ef502699879b3cf3e66b9b23f44290cbc64a27cee6012d2fa99e59257918d5e
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A systems paper and experience report describing a three-tier context infrastructure — an always-loaded constitution, specialized domain-expert agents, and on-demand specification documents — built while developing a 108,000-line C# system with Claude Code as the only code-generation tool."
  author: ["Aristidis Vasilopoulos"]
  abstract: "The paper argues that LLM-based agentic coding assistants lack persistent memory and that single-file manifests do not scale to large, multi-agent projects. It presents a three-component codified context infrastructure — a hot-memory constitution, 19 specialized domain-expert agents, and a cold-memory knowledge base of 34 on-demand specification documents — reports metrics across 283 development sessions with four observational case studies, and publishes the framework as an open-source companion repository."
  keywords: ["context engineering", "multi-agent systems", "context infrastructure", "agentic software engineering"]
---

This paper starts from the observation that AI coding agents have broad programming knowledge but no
project memory: each session begins unaware of prior sessions, established conventions or past
mistakes. Single-file manifests such as [[DefinedTerm/agents-md]], `CLAUDE.md` or `.cursorrules`
address this for small projects, but the author argues they do not scale — a 1,000-line prototype
can be described in one prompt, a 100,000-line system cannot. Where earlier empirical studies
characterize what developers write in such files, this paper asks what happens when a project's
knowledge outgrows a single file.

Its answer is a *codified context infrastructure*, defined as structured artifacts written
explicitly for machine consumption — documents whose primary audience is an AI agent rather than a
developer. It was developed iteratively while building a 108,000-line C# real-time multiplayer
simulation over 70 days of part-time work, with [[SoftwareApplication/claude-code]] as the sole
code-generation tool. The architecture has three tiers with different loading strategies: a single
Markdown **constitution** of about 660 lines loaded into every session (hot memory), holding code
standards, conventions, build commands, known failure modes and trigger tables that route tasks to
specialist agents by which files are being changed; **19 specialized agent specifications** totalling
about 9,300 lines, each a domain-expert persona in which over half the content is project-domain
knowledge rather than behavioural instruction; and a **knowledge base** of 34 subsystem specification
documents totalling about 16,250 lines (cold memory), served on demand through a
[[DefinedTerm/model-context-protocol]] retrieval server.

The author positions this as complementary to multi-agent coordination frameworks: those define how
agents coordinate, while this work structures the knowledge agents depend on — indexing knowledge
*about* code, such as design intent, constraints and failure modes, rather than the code itself. The
framework, including example agent specifications, the retrieval server and bootstrapping agents, is
published as an open-source companion repository.

## Key Points

- Across 283 development sessions the author records 2,801 human prompts, 1,197 agent invocations and
  16,522 autonomous agent turns — roughly six agent turns per human prompt — and 1,478 retrieval calls
  to the knowledge base across 218 sessions.
- The context infrastructure totals about 26,200 lines, 24.2% of the codebase's size; the author
  treats this knowledge-to-code ratio as a reflection of this project's complexity and domain, not as
  a target or finding.
- Specialist agents were usually created in response to observed failures rather than designed
  upfront: when debugging a domain repeatedly stalled or required re-explaining the same knowledge,
  it was faster to codify that knowledge into an agent specification and restart the task.
- Four observational case studies illustrate distinct roles for codified context: a save-system
  specification referenced in 74 sessions during which five persistence features were built with no
  save-related bugs; a UI-synchronization specification that let a later feature apply an established
  pattern on its first attempt; a retrieval query returning nothing, which exposed an undocumented
  subsystem that was then specified before refactoring; and a domain agent whose embedded knowledge
  helped resolve a determinism bug that had eluded five earlier attempts.
- Specification staleness was the primary failure mode: on at least two occasions outdated documents
  led agents to generate code conflicting with recent refactors, and the author stresses that agents
  trust documentation absolutely. A session-start hook that warns when source files change without a
  matching specification update partially automates the check.
- Maintenance overhead averaged about one to two hours per week — roughly five minutes per session in
  which a specification was affected, plus a biweekly review pass across all context documents.
- The paper distils six practitioner guidelines, among them that a basic constitution does heavy
  lifting from day one, that knowledge explained twice should be written down, and that agent
  confusion is a diagnostic signal that a specification is missing or stale.

## Notes

The author is explicit that this is a systems paper and experience report whose contribution is the
architecture rather than statistical evidence of effectiveness: the evaluation is a single developer
on a single project, relies on observational case studies rather than controlled experiments, and
makes no causal claims, with developer experience growth among the confounders that cannot be
isolated. The implementation is tied to Claude Code with MCP support, though the author argues the
principles — tiered knowledge, hot/cold separation and domain-specialist routing — apply to any agentic
coding tool that supports session-start configuration and on-demand retrieval. The author notes a
background in chemistry rather than software engineering, framing the project as a test case for
domain experts building software beyond their primary expertise with AI agents, and names controlled
benchmarking of each tier as the most immediate next step.

The paper mentions [[SoftwareApplication/conductor-gemini-cli-extension]] as addressing a similar
problem through persistent Markdown and a spec–plan–implement workflow, and describes its own work as
developed independently and concurrently, with a focus on knowledge organization portable across
agentic coding tools. The version extracted here is arXiv:2602.20478v1 [cs.SE].
