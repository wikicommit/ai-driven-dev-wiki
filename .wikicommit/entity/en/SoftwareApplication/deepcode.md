---
title: "DeepCode"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, agent-tooling, open-source]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.07921'
    hash: sha256:314c8fd358fe756fabd1a16577a270aadea8b7375da1f84868c4809b3eb32278
  - type: url
    url: 'https://github.com/HKUDS/DeepCode'
    hash: sha256:ea03a03982aee7bc2179cd3e301a3e7ab3cc8f4c37fc66f7b316183d6ea28db3
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source coding agent from researchers at The University of Hong Kong. It began as an agentic framework for synthesizing a complete code repository from a document such as a scientific paper, and since version 2.0 has been a general-purpose coding agent for repository work, with that paper-reproduction workflow kept as Paper2Code."
  applicationCategory: "Coding agent"
  author: "The University of Hong Kong"
---

DeepCode is an open-source agentic coding framework, published by researchers at The University of Hong Kong, for synthesizing a complete, executable code repository from a document — most centrally, reproducing a scientific paper's experiments as code using the paper as the sole specification. Its source code is published on GitHub at HKUDS/DeepCode under the MIT license.

The project's README describes a later rebuild: DeepCode v2.0 introduced a general-purpose coding agent framework for building, fixing, understanding and improving real software projects, and Paper2Code, the paper-reproduction workflow that was the project's original research direction, remains its dedicated workflow for research reproduction. The README names four kinds of depth the project aims for — context, execution, verification and continuity — and says it is designed not to make an agent look busier but to help finish real software engineering work more reliably.

## Capabilities

As a general coding agent, DeepCode reads and searches code, edits files, applies patches, runs commands and tests, and continues working from the results, keeping tool calls, execution progress and file changes visible. It has three clients — a terminal interface, a desktop app and a browser-based web interface — which connect to one shared local background service and share projects, sessions, models, skills, permissions and goals; closing a client leaves accepted work running, and another client can reconnect to the same task. Sessions are stored locally and keep tool calls, permission decisions, goals, model configuration and verification records alongside the conversation, and long conversations are shortened by [[DefinedTerm/compaction]].

For work that cannot be finished in one response, the user gives DeepCode a natural-language goal — a feature the README calls goal-driven Loop Engineering — and the agent keeps analyzing, implementing, verifying and repairing around it while the user can add information, revise the goal or its acceptance criteria, queue the next instruction, or pause, stop and resume it. Completion is evidence-driven: rather than one hard-coded rule, DeepCode selects evidence that fits the task, such as test results, build output, static checks, diagnostics or diffs, and a failed verification becomes input to the next repair. The README states that the working agent itself requests a complete or blocked outcome, and that DeepCode enforces ownership, lifecycle, permission and budget boundaries without pretending a generic host-side rule can validate every coding task.

Every project must be explicitly trusted before the agent executes in it, and each session runs in one of three [[DefinedTerm/permission-modes]] — ask, read only, or full access — with individual tools additionally set to allow, ask or deny. Other features include connecting a range of model providers with the user's own API key, reusable [[DefinedTerm/agent-skills]], local plugins, [[DefinedTerm/model-context-protocol]] servers, parallel agents working in isolated [[DefinedTerm/git-worktrees]] with conflicts shown explicitly rather than silently overwritten, delegation to [[SoftwareApplication/openai-codex]] or [[SoftwareApplication/claude-code]] as external subagents, and automations that run a saved instruction on demand or on a schedule through the same agent and permissions.

For paper reproduction, the framework accepts a target document in PDF or Markdown form and produces a repository through three phases: a Blueprint Generation phase that distills the document into a structured implementation blueprint (project file hierarchy, per-module component specifications, a verification protocol, and an execution-environment specification); a Code Generation phase that synthesizes files iteratively against that blueprint using a stateful memory of already-generated files (CodeMem) and a retrieval-augmented system (CodeRAG) that pulls in patterns from external repositories only when needed; and an Automated Verification phase that runs static analysis followed by sandboxed execution, feeding runtime errors back into an iterative repair loop. The README describes the Paper2Code architecture as a central orchestrating agent coordinating specialist agents for intent understanding, document parsing, code planning, code reference mining, code indexing and code generation.

On the PaperBench Code-Dev benchmark (20 ICML papers, graded by an automated judge), it is reported to score 73.5±2.8 on average, versus 43.3±1.1 for the best general-purpose LLM-agent baseline and 51.1±1.4 for a specialized scientific-code-agent baseline (PaperCoder); on a 5-paper subset, it scored 0.8541 versus 0.5871 for Claude Code and 0.5841 for Cursor — both run on the same base model as DeepCode, Claude Sonnet 4.5-thinking — and 0.3997 for Codex, which was run on GPT-5 Codex-high.

## Adoption & Ecosystem

The framework is evaluated specifically for scientific-paper reproduction and general document-to-software synthesis, and is compared in its publication, [[ScholarlyArticle/deepcode-open-agentic-coding]], against both general-purpose commercial coding agents (Cursor, Claude Code, Codex) and specialized scientific-code-reproduction tools (PaperCoder). The README cautions that its PaperBench results are specific to that benchmark and are not a general-purpose coding benchmark or a comparison against continuously updated products.

It reads project instructions from [[DefinedTerm/agents-md]] or DEEPCODE.md, and reads existing DeepCode and Claude-style skill directories without migrating them.
