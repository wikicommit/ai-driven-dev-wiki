---
title: "OpenAI"
type: "schema:Organization"
lang: en
tags: [agentic-coding]
sources:
  - type: url
    url: 'https://openai.com/index/introducing-codex/'
    hash: sha256:c899f94e6c00781777e4a0c930a154bee0271654282a1a6f195b368868a1366b
  - type: url
    url: 'https://openai.com/codex/'
    hash: sha256:d885d8a80478f4aecb76134aac46d1976013ff1a1cf8ecb1eead450eeac6d72a
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The company behind ChatGPT and [[SoftwareApplication/codex]], its software engineering agent. It releases coding agents under what it calls an iterative deployment strategy, and ships an agent guided by AGENTS.md files placed in a repository."
  url: "https://openai.com/"
---

OpenAI is the company behind ChatGPT and [[SoftwareApplication/codex]], its software engineering agent. Its relevance to this wiki is as one of the main vendors shaping agentic coding practice: it ships the agent, the models behind it, and — per its own launch post — an agent guided by [[DefinedTerm/agents-md]] files placed in a repository.

## History

The sources ingested here do not cover OpenAI's founding or corporate history. What they document is a release practice: Codex was launched on 16 May 2025 as a **research preview**, which OpenAI describes as being "in line with our iterative deployment strategy", with security and transparency prioritised in the design so users can verify outputs — a safeguard it calls increasingly important as models handle more complex coding tasks independently. Before that launch it had worked with a small group of external testers to understand how Codex performed across diverse codebases, development processes and teams, naming Cisco, Temporal, Superhuman and Kodiak among them.

## Activities & Products

Codex is the product covered here, launched as a cloud agent and later presented as one agent across ChatGPT, an IDE extension and [[SoftwareApplication/codex-cli]]. The models named in the launch post are `codex-1`, a version of OpenAI o3 optimized for software engineering, and a smaller variant derived from o4-mini released as the CLI default and as `codex-mini-latest` in the API.

OpenAI also uses the tool internally. The launch post reports that technical teams at OpenAI had started using Codex as part of their daily toolkit, most often to offload repetitive, well-scoped tasks such as refactoring, renaming and writing tests that would otherwise break focus, and equally for scaffolding features, wiring components, fixing bugs and drafting documentation — with teams building habits around triaging on-call issues, planning tasks at the start of the day, and offloading background work.

Its stated position on where this is heading is a two-mode convergence: real-time pairing and asynchronous task delegation collapsing into a single workflow across IDEs and everyday tools, with OpenAI predicting the asynchronous multi-agent mode will become "the de facto way engineers produce high-quality code". That is the company's own forecast rather than an observed outcome. OpenAI also says it is collaborating with partners to understand the implications of widespread agent adoption for developer workflows and for skill development across people, skill levels and geographies.
