---
title: "Shannon"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-framework, sandboxing, multi-agent]
sources:
  - type: url
    url: 'https://waylandz.com/ai-agent-book/%E7%AC%AC29%E7%AB%A0-Agentic-Coding/'
    hash: sha256:8d26acd2d82ab50470efb941ede6e3ad8e4fb4bae0f286b12e4c0dd3fbed6b2b
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An AI agent system whose source code serves as the reference implementation for the online book AI Agent 架构：从单体到企业级多智能体; its built-in file tools confine reads and writes to allowlisted directories, and it uses WASI as its primary sandbox."
  featureList: "Built-in file read tool with a size cap and a directory allowlist; file write tool flagged as requiring authorization, sandboxed and dangerous; WASI-based sandboxing; model configuration that lists coding-specialist models"
---

Shannon is an AI agent system whose source code the online book *AI Agent 架构：从单体到企业级多智能体* maps its concepts onto. The book's chapter on [[DefinedTerm/agentic-coding]] ends with a "Shannon Lab" section pointing readers to the Shannon files that correspond to the chapter's concepts, and uses Shannon's built-in file tools to show how an agent's access to a codebase can be limited, and the book's next chapter is introduced as showing how Shannon implements reliable background agents with Temporal.

## Capabilities

Shannon's file-reading tool, in its LLM service's built-in tools, takes a path and a maximum file size to read — 10 MB by default, adjustable between 1 and 100 MB — and refuses any path outside an allowlist made up of `/tmp`, the current working directory and, when the `SHANNON_WORKSPACE` environment variable is set, that workspace. The chapter reads this design as preventing oversized reads, keeping reads inside the workspace and temporary directories, and — through path normalization — preventing escape through symbolic links.

Its file-writing tool is marked as requiring authorization, sandboxed and dangerous, supports an `overwrite` mode (the default) and an `append` mode, and creates missing parent directories only when asked to.

According to the chapter, Shannon's architecture documentation names WASI as its primary sandbox mechanism, which the chapter credits with millisecond start-up, fine-grained control over capabilities such as the file system, network and time, and a small resource footprint.

## Adoption & Ecosystem

Shannon's model configuration lists a group of coding-specialist models — a dedicated code model alongside general and reasoning-oriented models — which the chapter uses to illustrate routing different coding tasks to different model tiers. The chapter also points to a Shannon document on multi-agent workflow architecture for how a coding agent is integrated into a multi-agent system.
