---
title: "Hermes Agent"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-architecture]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.14228'
    hash: sha256:c6ebed0a2e24b61491efe18f003cf6d6c018a671a732b3d6e331a5fe195a0e9d
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source AI agent from Nous Research that runs as a single Python process whose role is set by the entry point that launched it, fronting many messaging and IDE surfaces over one runtime and one persistence layer."
  applicationCategory: "AI agent"
  featureList: "Single-process multi-surface runtime; centralized per-action tool approval with three modes; pluggable memory and model-provider backends; SQLite session store with full-text search; cron scheduler and webhook subscriptions; SQLite-backed Kanban work queue"
  author: "Nous Research"
---

Hermes Agent is an open-source AI agent from Nous Research, built as a single long-lived Python process whose role is fixed by the entry point under which it was invoked. Its distribution exposes three console scripts: `hermes` for the CLI and gateway controller, `hermes-agent` for batch runs, and `hermes-acp` for an Agent Client Protocol adapter that lets external IDEs host Hermes much as Hermes's own gateway can host other agents. The result is many surfaces fronting one runtime and one persistence layer.

[[ScholarlyArticle/dive-into-claude-code]] uses it, alongside [[SoftwareApplication/openclaw]], as an independent point of comparison for [[SoftwareApplication/claude-code]], and characterizes it as sitting between the two: closer to OpenClaw in trust topology but closer to Claude Code in process topology. Where OpenClaw places a broker at the centre, the authors observe that Hermes answers the question of where to put the broker with no broker at all.

## Capabilities

The agent loop is a synchronous `while` inside `AIAgent.run_conversation`, gated on an iteration count defaulting to 90 plus a separate iteration budget; when that budget is exhausted a single tool-stripped summary call lets the agent deliver a closing message rather than terminate mid-thought. Tool files under `tools/` self-register at import time, so adding a tool requires only one registry call, and a single assistant message returning multiple tool calls is executed in parallel with a sequential fallback.

Tool authorization is centralized in one file and exposes three modes — manual, smart, and off — over an unconditional floor of hardline patterns that blocks destructive commands such as `rm -rf /`, `mkfs`, raw `dd` to block devices, fork bombs and system shutdown regardless of mode. The smart mode runs an auxiliary-LLM risk assessment, which an in-source comment attributes to OpenAI Codex's smart approvals as its design inspiration. Because Hermes spans many surfaces, the same approval flow is rendered four ways: a CLI prompt, gateway approval keyboards on Telegram, Discord and QQBot, an ACP permission round-trip for IDE clients, and a cron-only mode for unattended runs.

Five extension surfaces are described. Three sit at the same level as Claude Code's — general plugins with lifecycle hooks, bundled skills, and MCP servers configured in `config.yaml` — while two extend a different axis, letting Hermes swap whole memory and model-provider backends in place rather than intercept events around them. Hooks may be in-process Python callbacks or config-driven external shell commands, dispatched through one hook manager. When Hermes spawns a stdio MCP server, the child's environment is restricted to a small allowlist of system variables before launch and package names are screened against the OSV malware database.

Context management is one auxiliary-LLM summarizer with token-budget tail protection, preceded by a tool-output prune pass; the summary carries a "reference only" preamble telling the agent that the compaction is background context rather than new instructions and that persistent memory files remain authoritative. Before injection, context files such as `AGENTS.md`, `.cursorrules` and `SOUL.md` are scanned for injection patterns and invisible Unicode, and any hit replaces the file's content with a blocked marker.

Delegation goes through a `delegate_task` tool that spawns child agent instances in a thread pool. The parent blocks until children return summaries; concurrency is capped at three children by default and depth at one, leaf children cannot themselves delegate without opt-in, and children always run with persistent memory disabled so they can neither read nor write the parent's notes. Separately, a Kanban subsystem provides a SQLite-backed work queue in which multiple worker profiles claim, heartbeat and complete tasks, with stale-claim reclamation and an automatic block after two consecutive failed attempts.

## Adoption & Ecosystem

Session state and a multi-agent board are persisted to on-disk SQLite files rather than to a typed wire protocol, using a WAL-mode database with full-text search across all session messages and a parent-session chain recording compaction-triggered splits — which the analysing authors note gives cross-session search and concurrent-reader support without extra work. When the gateway restarts mid-conversation, sessions auto-resume on the next message arrival under transcript-freshness logic with a one-hour default window. A built-in cron scheduler and webhook subscription system let the agent run unattended on schedule expressions or external HTTP events, with cron sessions running with persistent memory disabled. The distribution also ships a background curator loop that reviews agent-created skills and archives stale ones without ever deleting, scoped so that bundled and hub-installed skills are off-limits.

Messaging surfaces are driven through a two-tier adapter system, with in-tree adapters plus a plugin tier covering Google Chat, IRC and Teams. The authors of the analysing paper note two places where the project's own documentation has drifted from its implementation — an approval-mode taxonomy and a delegation depth default — and state that they cite the source rather than the docs.
