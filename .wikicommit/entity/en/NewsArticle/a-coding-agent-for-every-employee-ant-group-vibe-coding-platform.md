---
title: "让每个员工都有一个 Coding Agent：蚂蚁 Vibe Coding 平台落地半年后的实践经验｜QCon 北京"
type: "schema:NewsArticle"
lang: en
tags: [qcon, vibe-coding, coding-agents, enterprise-ai-adoption]
sources:
  - type: url
    url: 'https://www.infoq.cn/article/zwsaRqiZ99H7l3y8G9Lc'
    hash: sha256:345f662823f0fe3a3b0a8d5580142ac85b98899805a40bb68b4069f997381efa
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An April 2026 InfoQ China announcement of a QCon Beijing 2026 talk by an Ant Group front-end engineer on Muse, an internal visual vibe-coding platform meant to let non-technical staff deliver websites and systems, and on what it took to move it from generating code to delivering it reliably."
  datePublished: "2026-04-11"
  publisher: "InfoQ"
---

The article ("A coding agent for every employee: lessons from half a year of Ant Group's vibe coding platform in production") is InfoQ China's announcement, dated 11 April 2026, of a talk in the "Coding Agent-driven new R&D paradigm" track at QCon Beijing 2026, held 16–18 April. The speaker, a front-end engineer at Ant Group who led a low-code team's move into AI, presents [[SoftwareApplication/muse]], an internal platform combining online visual [[DefinedTerm/vibe-coding]] with a coding agent so that people in non-technical roles can build applications and websites through conversation and visual editing. The article reproduces the talk outline, so its content is the speaker's own account.

The talk's argument is that once users move from trying the platform to using it in production, the core challenge is no longer whether the platform can generate something but whether it delivers stably. Its summary line is that coding matters less and less and delivery is what counts, and it closes on the claim that the key to making AI broadly usable is not a stronger model but a stronger delivery system.

## Key Points

- The platform is reported at more than 10,000 monthly active users, with more than 10,000 applications or runtimes running online.
- The challenges named at production scale are context bloat in long conversations and large projects, generation quality and consistency, deployment and security, and tasks interrupted when a user leaves partway.
- The overall approach is summarised as "framework constraints + a controlled toolchain + self-healing delivery".
- Six problem areas are listed: very long multi-turn conversations, very large projects and repositories, capability sprawl from skills, stability and deployment, ecosystem connections, and permissions and data.
- For long conversations the talk describes context engineering with "files as memory": layered memory, loading and unloading, and externalising long-term state into project files such as spec, runbook and `readme_for_agent` files so the agent can reliably pick work back up.
- For large repositories it argues that stuffing the whole repository into context is not sustainable, and instead builds a CodeMap — a project map of symbols, references, dependencies and entry points built from language services such as LSP and tsserver plus build dependency information — used with file read and write tools for incremental, bounded changes.
- Skills are loaded on demand after intent-based routing, and their output is written to files so it can be reused.
- Self-healing delivery works before, during and after generation: scaffolds and constraints so the default is correct, LSP, TSC and lint checks inside the agent loop, and silent repair of build errors plus continuation in an offline container with a notification when a user has left.
- The speaker names three underlying requirements: MuseJS, a convention-based full-stack framework positioned as the platform's counterpart to Next.js; a sandbox with isolation, controlled tool calls, auditability and offline execution; and an integrated database positioned against Supabase, secure by default.
- On trends, the speaker expects agent-first documentation such as `readme_for_agent.md` to become a key asset while GUIs may decay, collaboration to be driven by task and change trajectories rather than only pull requests, and a supervisor to schedule multiple agents in containers until a task succeeds.
- The pain points are framed as trade-offs: low barrier to entry against enterprise complexity, freedom against control, success rate against cost and latency, automatic repair against explainability, and ecosystem integration against security and compliance.

## Context

The talk treats vibe coding as a production delivery problem for non-developers rather than a developer productivity aid, which sets it apart from much of the writing this wiki collects under [[DefinedTerm/vibe-coding]]. Its "files as memory" approach and the CodeMap index connect to [[DefinedTerm/context-engineering]]. All usage figures are the speaker's own, given in a pre-conference outline.
