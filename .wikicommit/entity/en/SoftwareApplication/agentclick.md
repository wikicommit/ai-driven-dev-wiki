---
title: "AgentClick"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, human-oversight, agent-skills]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.16520'
    hash: sha256:2601c1408563f747b2ac732af43342b6d4d14231aace9b4a2e0aa4d33ba3f674
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A browser-based review layer for terminal AI agents, run as a localhost npm server paired with a set of Markdown skills, that replaces raw terminal output with task-specific interfaces for inspecting and editing an agent's proposed emails, plans, code changes, memory and execution traces before they take effect."
  applicationCategory: "Agent review interface"
  featureList: "Task-specific browser review UIs for email, plans, code, memory and trajectories; paragraph- and hunk-level editing; pre-execution constraint injection; reason-tagged preference capture to a memory file; HTTP access for remote and cross-device review"
---

AgentClick is a review layer that sits between a terminal-based AI agent and the person supervising it. It runs as a localhost npm server paired with a skill-based plugin, and exposes a browser interface in which the agent's proposals are presented as structured artifacts rather than as terminal text. When the agent reaches a consequential step it submits a proposal to the backend, which creates a review session and surfaces it in the browser; the user can approve it, edit it directly, delete content, adjust constraints or request a targeted rewrite, and the result is returned to the agent, which incorporates the feedback and continues.

The design is described in [[ScholarlyArticle/agentclick]], which frames the tool as improving collaboration rather than merely gating execution — the intervention happens at the level of the artifact under review, which its authors argue matters most when an agent's output is largely correct but needs a localized change. Because intermediate artifacts are surfaced before final execution, the same flow doubles as a way to track progress and locate errors early.

## Capabilities

Five task-specific review interfaces are provided, on the stated principle that different agent outputs require different review affordances. The email interface combines inbox browsing, full message rendering and reply drafting, with per-section rewrite, edit and delete controls and sending gated on explicit confirmation. The plan interface presents a proposed workflow upfront as typed step cards — distinguishing tool calls, file operations and code execution — which can be edited in place, reordered, constrained or removed before execution begins. The code interface shows each proposed change as a review artifact with the command, a natural-language explanation, the affected files and a unified diff, and lets users expand a file for full context, approve individual hunks, annotate specific lines, or request a partial rewrite. The memory interface lists loaded entries, surfaces proposed updates for review before they are committed, and lets users load or unload memory files from a single panel. The trajectory interface renders the execution trace with tool calls, failed attempts and error recoveries highlighted distinctly, and lets users annotate steps with guidance that is written to memory.

Integration uses a hierarchy of Markdown skills rather than an SDK. A main skill handles bootstrapping and dispatch — instructing the agent how to initialize or connect to the local server, establishing the protocol for submitting proposals and receiving results, and routing to the right sub-skill by task intent — while sub-skills define the payload schema, review actions and result handling for each domain. The authors give two reasons for this: skills need no instrumentation of the agent's codebase and add no runtime dependencies, and any agent able to read and follow Markdown instructions can adopt the layer without modification.

Preferences persist across sessions. When a user edits or deletes part of an artifact and supplies an explicit reason, the system records that feedback to a structured memory file the agent incorporates in later runs, which the authors describe as most useful for recurring tasks such as email where the same stylistic correction would otherwise be repeated.

## Adoption & Ecosystem

The interface is served over HTTP, which the authors present as the answer to agents running on remote or headless infrastructure — cloud VMs, shared servers or containers — where users would otherwise interact through text channels with no convenient access to the terminal. Their illustration is a user whose agent runs on a Mac Mini receiving an approval prompt in Discord, opening the AgentClick URL on a phone, reviewing the draft or plan, editing it and confirming, without touching the terminal.

[[SoftwareApplication/claude-code]] and [[SoftwareApplication/openclaw]] are the two agents named as adopters in the paper's walkthroughs: Claude Code for the plan-review and email-rewrite tasks, and OpenClaw for a remote review carried out from a mobile browser against an agent running on a server behind a tunnel. The code is published on GitHub.
