---
title: "Routa"
type: "schema:SoftwareApplication"
lang: en
tags: [multi-agent, agent-orchestration, coding-agents, agent-protocols, harness-engineering]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/coding-agent-platform-engineering/'
    hash: sha256:8dfe0d1a99160baa5c9e267af55b3724ec49f6cd505455926157bf819fb2a673
  - type: url
    url: 'https://www.phodal.com/blog/harness-engineering/'
    hash: sha256:c7eb3fe986b891735c956a0430dbd40b0a73c9b4a1a3852ef3f9063202490339
  - type: url
    url: 'https://www.phodal.com/blog/routa-harness-engineering-builtin-platform/'
    hash: sha256:4ba80d8b7c39b0795402b9a0c3ede0acef5af2849700b26983a9c5d2c5201060
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An open-source multi-agent orchestration platform for coding agents that combines an external orchestrator with an optional Workspace Agent mode. It connects agents through A2A, MCP, ACP and REST and runs coding agents such as Claude Code, OpenCode, Gemini and Codex as ACP processes."
  applicationCategory: "Multi-agent orchestration platform"
  author: ["Phodal Huang"]
---

Routa is an open-source multi-agent orchestration platform, published as the `routa-js` repository,
that [[BlogPosting/platform-engineering-where-everything-is-a-coding-agent]] presents as a practical
reference for orchestrating coding agents. It uses a hybrid of the two orchestration modes that post
describes: an external orchestrator that drives coding agents as separate ACP processes, and a
Workspace Agent that can act as a macro-coordinator over sub-agents as an optional mode.

Its author, Phodal Huang, later announced a desktop version in
[[BlogPosting/routa-desktop-release-ai-coding-workbench-with-built-in-harness-engineering]], describing
Routa there as an AI coding collaboration workbench with built-in harness engineering and as the first
fairly complete product form of his formula "Harness engineering + Coding Agent + Kanban = an AI
automated R&D workbench". That post says Routa aims to reconnect the flows of tasks, responsibilities
and evidence, rather than to be a chat-style coding agent or only a container for multiple agents.

## Capabilities

The architecture the platform-engineering post describes has five layers. A protocol gateway accepts
[[DefinedTerm/agent2agent-protocol]] for federation, [[DefinedTerm/model-context-protocol]] for tools,
the [[DefinedTerm/agent-client-protocol]] for processes and REST for management. Below it, an
orchestration engine layer holds an Orchestrator that decomposes tasks, manages dependencies and
schedules agents; an EventBus that carries event-driven communication and handles agents' reports to
their parent; and a Skill Matcher that matches agents to tasks by the task's characteristics. A state
layer keeps tasks, agents, notes and traces, an ACP process manager spawns, prompts, cancels and
subscribes to agents, and the bottom layer is the coding agents themselves — the post names
[[SoftwareApplication/claude-code]], [[SoftwareApplication/opencode]], Gemini and Codex.

Work is divided among three roles with explicit boundaries: a Coordinator that plans, decomposes and
summarises but does not write code directly, an Implementor that builds each task without widening its
scope, and a Verifier that accepts and reviews work but does not modify code. That post gives Claude
(marked "smart") as the typical provider for the Coordinator and Verifier, and OpenCode (marked "fast")
for the Implementor.

The desktop-release post centres on Routa Kanban, which it describes as at once a task board, the
interface for assigning work to agents, and a task state machine with built-in quality gates, stage
constraints and domain specialists. Its columns — `backlog`, `todo`, `dev`, `review`, `done` and
`blocked` — work as entry and exit gates: a card entering `backlog` must carry machine-readable YAML
with a problem statement, acceptance criteria, scope, dependencies and an INVEST check; `todo` asks for
an execution plan, key files, a dependency plan and risks; `dev` asks whether the work is ready to code
and requires development deliverables after implementation; `review` checks that evidence is complete,
verification independent and scope contained; and `done` requires an approved review result. A
downstream column can send an incomplete card back upstream.

Cards are moved between columns by lane-specialist agents, each doing only its own column's work,
verifying the upstream output first and handing off explicitly with `move_card`. The post lists a
KanbanTask Agent that splits natural-language requirements into backlog-ready cards without
implementing them; a Backlog Refiner that turns rough cards into executable stories; a Todo
Orchestrator that checks backlog output and adds the execution plan; a Dev Crafter that implements,
commits and attaches development evidence; a QA Frontend specialist that adds visual-regression and
screenshot evidence for UI work; a Review Guard that acts as the final quality gate, independently
checking acceptance criteria, tests, Git state, scope and the Entrix budget; a Blocked Resolver that
reroutes blocked work; and a Done Reporter that writes a completion summary. A PR Publisher prepares
branches and opens pull or merge requests as a delivery-side specialist outside the basic board flow,
and a general Kanban Workflow specialist takes over only on columns that have no lane specialist.

Around Routa the author grew several further components: Entrix, which turns quality rules,
architecture constraints and verification steps into executable guards; a Harness Monitor that keeps
watching quality and change while several agents work on one codebase; a Harness Dashboard that
visualises those signals; and Routa Kanban itself.

## Adoption & Ecosystem

The desktop-release post reports that Routa has close to 500,000 lines of code, almost all of it
generated by AI.


The platform-engineering post lists the practices the design rests on: external systems trigger tasks through webhooks or
A2A; providers are pluggable, so the same role can be filled by different coding agents and switched at
runtime; all state changes pass through the EventBus to support asynchronous collaboration; and role
instructions and behavioural boundaries are defined as Skills written in Markdown with YAML
frontmatter.

[[BlogPosting/harness-engineering-practice-guide-three-principles]] uses Routa.js as a case study in
[[DefinedTerm/harness-engineering]]. It describes the project as both the working environment for AI
agents and a codebase that depends on those agents taking part in its own development, with several
agents — it names [[SoftwareApplication/kiro]], [[SoftwareApplication/github-copilot]], Augment and
Claude Code — collaborating in the same repository under shared engineering rules and quality gates.
That post sorts the project's practices under three headings:

- System legibility: an [[DefinedTerm/agents-md]] file sets coding standards, testing strategy, Git
  discipline and the co-author format for AI commits, and Specialist configurations define each
  agent's role and boundaries so that roles such as Developer and Verifier follow the process.
- Engineering defences: two layers of Git hooks, a fast pre-commit check and a pre-push check that
  returns structured error feedback, and a lint policy that lets some rules drop to warnings so that
  multi-agent collaboration is not blocked while the problems are still recorded for follow-up.
- Automated feedback loops: an Issue Enricher prepares context and proposes solutions for new issues; a
  Copilot Complete Handler moves draft pull requests to ready-for-review and triggers a review by an
  Augment agent; an Issue Garbage Collector periodically clears stale issues, with local issue files
  providing persistent context; and a Kanban system triggers agent tasks and requires verifiable
  artifacts such as test results or code diffs.
