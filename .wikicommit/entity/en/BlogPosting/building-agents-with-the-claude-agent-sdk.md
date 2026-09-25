---
title: "Building agents with the Claude Agent SDK"
type: "schema:BlogPosting"
lang: en
tags: [agent-architecture, agent-tooling, context-engineering, verification]
sources:
  - type: url
    url: 'https://claude.com/blog/building-agents-with-the-claude-agent-sdk'
    hash: sha256:895d1a97d551333d37c154b093d44ddda469401d6c2596c7a363373e974754a4
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Anthropic's post announcing that the Claude Code SDK is renamed the Claude Agent SDK, arguing that the harness behind Claude Code can power general-purpose agents. It organises agent design around a loop of gathering context, taking action and verifying work, and maps SDK features onto each stage."
  author: ["Thariq Shihipar"]
  datePublished: "2025-09-29"
  publisher: "[[Organization/anthropic]]"
---

This post from [[Organization/anthropic]] announces that the Claude Code SDK is being renamed the
[[SoftwareApplication/claude-agent-sdk]], and argues for the new name. Its case is that
[[SoftwareApplication/claude-code]], which Anthropic originally built for developer productivity, has
become far more than a coding tool: Anthropic reports using it internally for deep research, video
creation and note-taking, and says it has begun to power almost all of the company's major agent
loops. The harness underneath it can therefore power many other kinds of agent, and the rename is
presented as reflecting that broader scope.

The post's central design principle is to give the agent a computer. Claude Code works because
Claude has the tools programmers use every day — finding files, writing and editing them, linting,
running and debugging code, iterating until the code succeeds — and the post argues that the same
access to a terminal is what makes Claude effective at non-coding digital work as well. It then
proposes a way of thinking about any agent built this way: a feedback loop of **gather context → take
action → verify work → repeat**, which it illustrates throughout by sketching how an email agent might
be built on the SDK.

## Key Points

- The Claude Code SDK is renamed the Claude Agent SDK, because the agent harness that powers Claude
  Code can also power other types of agents; the post suggests finance, personal-assistant,
  customer-support and deep-research agents as examples.
- The key design principle is to give agents a computer so that they can work the way humans do,
  running bash commands and editing, creating and searching files.
- Agents often operate in a loop of gathering context, taking action and verifying work, and that loop
  is offered as a way to decide which capabilities an agent should be given.
- For gathering context, the folder and file structure an agent works in becomes a form of
  [[DefinedTerm/context-engineering]]: the agent decides how to load large files by using tools such as
  `grep` and `tail`. The post calls this [[DefinedTerm/agentic-search]].
- Semantic search is described as usually faster than agentic search but less accurate, harder to
  maintain and less transparent; the post recommends starting with agentic search and adding semantic
  search only when faster results or more variations are needed. This is Anthropic's recommendation,
  not a measured comparison.
- Subagents are supported by default and are useful for two reasons: parallelisation, and managing
  context, since each uses its own isolated context window and sends only relevant information back to
  the orchestrator (see [[DefinedTerm/sub-agent-architecture]]).
- The SDK's compact feature automatically summarises previous messages as the context limit approaches,
  and is built on Claude Code's `/compact` slash command (see [[DefinedTerm/compaction]]).
- Tools are prominent in Claude's context window and are therefore the primary actions Claude will
  consider, so the post advises designing them deliberately, for context efficiency, as the agent's
  primary and most frequent actions.
- Code generation suits agents because code is precise, composable and reusable; the post cites file
  creation in Claude.ai, which relies entirely on Claude writing Python scripts, as an example.
- [[DefinedTerm/model-context-protocol]] servers give standardised integrations to external services,
  handling authentication and API calls, so an agent can use services such as Slack or Asana without
  custom integration code.
- Agents that can check and improve their own output are presented as fundamentally more reliable.
  The post names three verification approaches: clearly defined rules with feedback on which failed
  and why (with code linting as the example, and linted TypeScript preferred over plain JavaScript for
  the extra feedback layers); visual feedback from screenshots or renders; and
  [[DefinedTerm/llm-as-a-judge]], which it calls generally not very robust and costly in latency,
  though helpful where any performance boost is worth the cost.
- To improve an agent, the post recommends reading its output closely, especially its failures, and
  asking whether it has the right tools; where performance varies as features are added, it recommends
  building a representative test set for programmatic evaluations based on customer usage.

## Context

The post presents itself as a follow-on to Anthropic's earlier writing on building effective agents,
and its recommendations are the best practices that emerged from Anthropic's own teams deploying the
SDK rather than the results of a comparative study. It is also a vendor describing its own product, so
its claims about what the SDK makes easier are the vendor's. It uses "agent harness" for what Claude
Code provides around the model (see [[DefinedTerm/agent-harness]]), and treats the SDK as a way of
handing that harness to other agents.
