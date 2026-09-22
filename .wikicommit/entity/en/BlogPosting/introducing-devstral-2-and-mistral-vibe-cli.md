---
title: "Introducing: Devstral 2 and Mistral Vibe CLI."
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, coding-tools, open-source, cli]
sources:
  - type: url
    url: 'https://mistral.ai/news/devstral-2-vibe-cli'
    hash: sha256:2138589678ecaf64d2613d8944af216e4e3b69049df0e348b80da6cd73da9788
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Mistral AI's December 2025 announcement of Devstral 2, an open-weight coding model family released in a 123B and a 24B size, together with Mistral Vibe CLI, an Apache 2.0 terminal coding agent built for those models. The post argues that compact open models can match much larger competitors on agentic coding work while conceding that a gap with closed-source models persists."
  author: "Mistral AI"
  publisher: "Mistral AI"
  datePublished: "2025-12-09"
---

*Introducing: Devstral 2 and Mistral Vibe CLI.* is Mistral AI's announcement, published on
9 December 2025, of two releases made together: Devstral 2, a coding model family shipped in a
123B and a 24B size, and Mistral Vibe CLI, a command-line coding agent built to run on them. The
post presents permissive licensing as part of the point — Devstral 2 under a modified MIT license,
Devstral Small 2 and the CLI under Apache 2.0 — and describes that choice as intended to
accelerate what it calls distributed intelligence.

The bulk of the post is a performance argument made on Mistral's own figures, and its recurring
theme is size. Both models are presented as substantially smaller than the open competitors they
are compared against while scoring at or above them, which the post offers as evidence that
compact models lower the hardware barrier for developers, small businesses and hobbyists without
giving up capability. Notably, the post does not claim parity with closed models: it reports that
a human evaluation preferred Claude Sonnet 4.5 over Devstral 2 by a clear margin and states
directly that a gap with closed-source models persists.

The second half turns to tooling. Mistral Vibe CLI is described as the native agent for these
models — an open-source terminal assistant that reads and edits a codebase through natural
language, integrates into an IDE through the Agent Communication Protocol, and is configured
through a local file rather than a hosted console. Together the two releases are presented as a matched
pair — Mistral's own model and Mistral's own agent for [[DefinedTerm/agentic-coding]] work, which
the post describes as enabling end-to-end code automation — alongside partnerships that put the
models into third-party agent tools.

## Key Points

- The post announces Devstral 2 in two sizes — Devstral 2, described as a 123B-parameter dense transformer, and Devstral Small 2 at 24B — both supporting a 256K context window, with Devstral 2 under a modified MIT license and Devstral Small 2 under Apache 2.0.
- Mistral reports Devstral 2 at 72.2% and Devstral Small 2 at 68.0% on [[Dataset/swe-bench-verified]]. These are the vendor's own reported figures in its own launch post, not an independent evaluation.
- The post's claim that Devstral 2 is up to 7x more cost-efficient than Claude Sonnet at real-world tasks is Mistral's own, and the post states it without setting out the methodology behind it.
- Mistral describes a human evaluation run by an independent annotation provider with tasks scaffolded through Cline, reporting a 42.8% win rate against 28.6% loss versus DeepSeek V3.2 — while also reporting that Claude Sonnet 4.5 remained significantly preferred, which the post itself reads as a persisting gap with closed-source models.
- Two endorsements are quoted, from Cline and from Kilo Code. Both are named in the same post as partner tools Mistral worked with to distribute the model, so they are partners' statements rather than independent assessment.
- The post claims Devstral 2 can explore codebases and orchestrate changes across multiple files while holding architecture-level context, tracking framework dependencies, detecting failures and retrying with corrections — capabilities it associates with bug fixing and legacy modernization. The backing offered is Mistral's own description of the model.
- Mistral Vibe CLI is presented as an open-source, Apache 2.0 command-line coding assistant that provides an interactive chat interface with tools for file manipulation, code searching, version control and command execution, and that integrates into an IDE through the Agent Communication Protocol.
- The CLI's described features include project-aware context assembled from the file structure and Git status, `@` autocomplete for file references, `!` for shell commands, slash commands for configuration, persistent history, programmatic invocation for scripting, a toggle for auto-approval of tool execution, and tool permissions and local model providers configured through a `config.toml`.
- The claim that multi-file orchestration can halve PR cycle time is Mistral's own marketing claim in this post, offered with no supporting measurement.
- On deployment, the post states Devstral 2 is optimized for data center GPUs and needs a minimum of four H100-class GPUs, while Devstral Small 2 is built for single-GPU operation and also runs CPU-only; it recommends a temperature of 0.2.

## Context

This is Mistral's second Devstral announcement, and the first release has its own page at
[[BlogPosting/devstral]]. What *this* post establishes about that lineage is only the naming: it
presents Devstral 2 and Devstral Small 2 as a next-generation family, without describing the
earlier release or restating what it claimed.

The post is a vendor launch announcement and should be read as one: every benchmark figure, cost
comparison and capability claim in it is Mistral's own, and the two quoted endorsements come from
tools Mistral partnered with for the launch. The one place the post argues against its own
interest — the Claude Sonnet 4.5 comparison — is also the only figure in it that a reader has no
commercial reason to discount.

Its tooling half announces [[SoftwareApplication/mistral-vibe-cli]], and what the post itself
emphasises about that release is licensing and deployability: the agent under Apache 2.0, the
models openly licensed alongside it, and both runnable outside a hosted service.
