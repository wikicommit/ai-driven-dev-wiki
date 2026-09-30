---
title: "Muse"
type: "schema:SoftwareApplication"
lang: en
tags: [vibe-coding, coding-agents, low-code, enterprise-ai-adoption]
sources:
  - type: url
    url: 'https://www.infoq.cn/article/zwsaRqiZ99H7l3y8G9Lc'
    hash: sha256:345f662823f0fe3a3b0a8d5580142ac85b98899805a40bb68b4069f997381efa
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "Ant Group's internal visual AI coding platform, combining online visual vibe coding with a coding agent so that employees in non-technical roles can build deliverable websites, applications and systems through conversation and visual editing."
  applicationCategory: "Visual AI coding platform"
  author: "Ant Group"
---

Muse is an internal AI coding platform at Ant Group. It is described in
[[NewsArticle/a-coding-agent-for-every-employee-ant-group-vibe-coding-platform]], InfoQ China's
announcement of a talk scheduled for QCon Beijing 2026 by a front-end engineer whose team built the
platform; what is known of it here comes from that announcement's abstract and the announced talk
outline. It is positioned as online visual [[DefinedTerm/vibe-coding]] plus a coding agent, aimed at
letting people in non-technical roles produce applications and websites through "conversation + visual
editing" rather than at making engineers faster.

The outline describes a user journey running from a one-sentence requirement through generated pages
and features, adjustment, connecting data and permissions, publishing, and then running and iterating.
It argues that a GUI still matters for lowering the barrier to starting and making results visible, but
that the design is "results first", because users care whether the output is stable and shareable
rather than about the code. The announcement states that the platform has passed 10,000 monthly active
users and more than 10,000 online applications or runtimes.

## Capabilities

According to the announcement, the approach combines framework constraints, a controlled toolchain and
self-healing delivery. The outline describes layered memory for long conversations, with long-term state
externalised into project files — spec, runbook and `readme_for_agent` files — so that the agent can
reliably resume; a CodeMap for large projects, a project map of symbols, references, dependencies and
entry points built from language services such as LSP and tsserver together with build dependency
information, used with file read and write tools for incremental changes within controlled boundaries;
and skills loaded on demand according to the task's routed intent, with their output written to files
for reuse.

The outline presents delivery as guarded at three stages: scaffolds, constraints and best practices
beforehand so the default output is correct; LSP, TSC and lint checks inside the agent's loop while code
is generated; and afterwards, silent repair of build failures and continuation in an offline container,
with a notification, when the user has left partway through a task.

It also names three components as hard requirements underneath the platform: MuseJS, a convention-based
full-stack framework positioned as a counterpart to Next.js and designed to be agent-friendly; a sandbox
providing isolation, controlled tool calls, auditability and replay, and offline execution; and an
integrated database, positioned against Supabase, that is secure by default.

## Adoption & Ecosystem

The announced outline describes hosting on internal and external networks with independent domains,
connections to working tools — it names DingTalk, Yuque, project management, ODPS and code repositories —
and integrated permissions and data, including changing database tables through conversation. It frames
the platform's open problems as trade-offs between low barrier to entry and enterprise complexity,
freedom and control, success rate and cost or latency, automatic repair and explainability, and
ecosystem integration and compliance.
