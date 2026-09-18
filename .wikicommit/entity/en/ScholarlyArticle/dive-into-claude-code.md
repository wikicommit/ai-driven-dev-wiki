---
title: "Dive into Claude Code: The Design Space of Today's and Future AI Agent Systems"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, coding-tools, agent-architecture]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.14228'
    hash: sha256:c6ebed0a2e24b61491efe18f003cf6d6c018a671a732b3d6e331a5fe195a0e9d
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A source-level architectural study of Claude Code that frames production coding agents as answers to a recurring set of design questions, traces five human values and thirteen design principles to specific implementation choices, and contrasts those answers with the open-source agent systems OpenClaw and Hermes Agent."
  author: ["Jiacheng Liu", "Xiaohan Zhao", "Xinyi Shang", "Zhiqiang Shen"]
  datePublished: "2026"
  keywords: ["Claude Code", "agent architecture", "design space", "coding agents", "permission systems", "context management", "OpenClaw", "Hermes Agent"]
---

This paper analyses [[SoftwareApplication/claude-code]] from its publicly available TypeScript source (a v2.1.88 extraction of roughly 1,884 files and 512K lines) and argues that a production coding agent is best understood as one set of answers to a recurring set of design questions: where reasoning sits relative to the harness, how many execution engines are needed, what safety posture to adopt by default, what resource is the binding constraint, how the extension surface is partitioned, how work is delegated, and how sessions persist. The authors motivate these answers by identifying five human values they read out of Anthropic's published material — human decision authority, safety/security/privacy, reliable execution, capability amplification, and contextual adaptability — and tracing them through thirteen design principles to specific files and functions.

The architecture they describe is a small reasoning core inside a large deterministic harness. A single `queryLoop()` async generator serves every surface (interactive CLI, headless CLI, SDK, IDE), and the model's only interface to the outside world is a structured tool-use protocol the harness validates before execution, so reasoning and enforcement occupy separate code paths. Around that loop sit the subsystems that make up most of the implementation: a [[DefinedTerm/deny-first-permission-evaluation]] system with seven permission modes and an optional ML classifier, a five-layer [[DefinedTerm/compaction]] pipeline, four extension mechanisms ordered by context cost (MCP servers, plugins, skills, hooks), subagent delegation returning summaries only, and mostly append-only JSONL session transcripts.

The paper then contrasts Claude Code with two independent open-source systems, [[SoftwareApplication/openclaw]] and [[SoftwareApplication/hermes-agent]], across six dimensions, arguing that the same design questions are stable while the answers vary with deployment context. It closes with six open directions and with a concern the authors raise repeatedly: the architecture amplifies what a developer can do in the short term but offers limited mechanisms that explicitly support long-term human understanding, codebase coherence, or the developer pipeline.

## Key Points

- The authors treat the harness, not the model, as where most of the engineering lives: they relay a community estimate that about 1.6% of the codebase is AI decision logic and the remaining 98.4% operational infrastructure, and read the architecture as investing in deterministic infrastructure rather than decision scaffolding.
- A single `queryLoop()` function executes regardless of surface; only the rendering and user-interaction layer varies. The authors contrast this with systems that use mode-specific engines.
- The default safety posture is deny-first with human escalation: deny rules override ask rules override allow rules, a deny rule wins even when an allow rule is more specific, and unrecognized actions are escalated rather than allowed silently.
- Seven permission modes are identified (plan, default, acceptEdits, auto, dontAsk, bypassPermissions, and an internal-only bubble mode for subagent escalation), forming what the authors call a graduated autonomy spectrum.
- Seven independent safety layers are enumerated, any one of which can block a request: tool pre-filtering, deny-first rule evaluation, permission-mode constraints, the auto-mode classifier, shell sandboxing, non-restoration of session permissions on resume, and hook-based interception.
- The context window is identified as the binding resource constraint, managed by five shapers that run in sequence before every model call — budget reduction, snip, microcompact, context collapse, and auto-compact — each escalating only when cheaper strategies prove insufficient.
- Four extension mechanisms are distinguished by what they uniquely provide and what they cost in context: hooks are zero-context by default, skills low (descriptions only), plugins medium, and MCP servers high (tool schemas). The paper counts 27 hook events, of which five participate directly in the permission flow.
- Subagents run in isolated context windows with independently assembled tool sets and return only summary text to the parent, with each subagent's conversation written to a separate sidechain transcript so it does not inflate the parent's session file.
- Session transcripts are mostly append-only JSONL, and resume and fork deliberately do not restore session-scoped permissions — the authors read this as treating sessions as isolated trust domains and accepting user friction to avoid carrying stale trust into a changed context.
- The comparison with OpenClaw and Hermes Agent is used to argue that the three systems place the trust boundary differently: Claude Code between the model and the execution environment, OpenClaw at the gateway perimeter, and Hermes between the two, with per-action approvals rendered across many surfaces.
- The authors note the three systems compose rather than compete: OpenClaw can host Claude Code as an external coding harness through the Agent Client Protocol, and Hermes sits on both sides of that host/guest split.
- The paper argues defense in depth rests on an independence assumption its layers do not fully satisfy, citing security research that commands with more than 50 subcommands fall back to a single generic approval prompt because per-subcommand parsing caused UI freezes.

## Notes

The authors grade their own claims at three evidence tiers — product-documented (official Anthropic documentation), code-verified (specific files and functions in the extracted TypeScript, which they call their strongest tier), and reconstructed (community analysis, structural comparison, or inference from code patterns, stated with hedging). They are explicit about the limits this imposes: the analysis reflects a single static snapshot whose feature flags create build-time variability, and source code cannot confirm design intent, which flags are enabled in production, or runtime prevalence.

Several of the paper's sharpest observations are about the human side rather than the code. It relays Anthropic's finding that users approve roughly 93% of permission prompts as evidence that interactive confirmation is behaviorally unreliable as a sole safety mechanism (see [[DefinedTerm/approval-fatigue]]), and longitudinal data showing auto-approve rates rising from about 20% below 50 sessions to over 40% by 750 sessions. On long-term capability the authors gather external findings — a randomized trial in which AI tools made developers slower despite a perceived speed-up, a causal analysis reporting increased code complexity after Cursor adoption, an EEG study reporting weakened neural connectivity among LLM users — and are careful to say this evidence motivates the question without targeting Claude Code's architecture specifically.
