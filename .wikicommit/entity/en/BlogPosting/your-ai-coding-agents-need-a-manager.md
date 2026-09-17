---
title: "Your AI coding agents need a manager"
type: "schema:BlogPosting"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/coding-agents-manager/'
    hash: sha256:fc697c3fcc830075a1a6b6751a1f242d4b6ff4ea9a385c1ec60a0c6f8a6e50a1
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Addy Osmani's argument that as AI coding agents take on more background, asynchronous work, the highest-leverage developers act as 'async-first managers' orchestrating a small fleet of parallel agents, and that engineering-management skills — clear scoping, delegation, verification loops, and async check-ins — transfer directly to doing that well."
  author: "Addy Osmani"
  datePublished: "2026-01-08"
---

This post argues that as AI coding agents increasingly do meaningful work in the background — running in isolated environments and returning something reviewable, often a pull request — the bottleneck shifts away from "can the agent write code?" and onto "should we build this?" and "can I manage multiple agents doing so effectively?" It frames the resulting posture as being an "async-first manager" running a small fleet of parallel coding agents, and argues that the skills that make someone a strong tech lead or engineering manager transfer directly to doing this well, because AI coding at scale stops being a prompting problem and becomes a management problem.

The post sets out a mental model of two modes run side by side: local, high-touch sessions where a developer stays [[DefinedTerm/human-in-the-loop]] for architecture decisions, tricky refactors, product nuance, and ambiguous requirements; and cloud or background sessions that run asynchronously on bounded tasks such as straightforward features, migrations with clear patterns, test generation, documentation updates, dependency bumps, and targeted refactors.

## Key Points

- Credits a viral thread from Boris Cherny, Claude Code's creator, with making the shift feel concrete: he is reported to run five [[SoftwareApplication/claude-code]] sessions locally in terminal tabs, another five to ten in the browser, and to start sessions from his phone to check on later.
- Cites Simon Willison's view that the natural bottleneck in running parallel coding agents is reviewing their output rather than generating it, and that the value of firing off parallel tasks holds only if a developer is honest about their own attention span and picks tasks that don't overload it.
- Sets out four manager skills the post argues transfer directly to directing coding agents: clear task scoping (a brief covering the outcome, context, constraints, non-goals, acceptance criteria, integration notes, and a verification plan); delegation (deciding what to fully hand off, what to delegate with checkpoints, and what to keep for human judgment, such as system architecture and security-critical design decisions); running a [[DefinedTerm/verification-loop]] (requiring test-suite output, passing lint and typecheck, added tests for behavior changes, and a structured "PR packet"); and async check-ins (a fixed status format and check-in cadence, likened to managing a distributed team across time zones).
- Describes GitHub's Copilot coding agent as positioning itself as an asynchronous background agent that opens a draft pull request, works in the background, and then requests review where a human can comment and have it iterate, and reports that GitHub previewed "Agent HQ" as a control plane for coordinating multiple third-party coding agents in one place, including running them in parallel on the same tasks to compare outputs.
- Attributes to [[Organization/anthropic]]'s own best-practices guidance for Claude Code the claims that specificity up front materially improves an agent's success rate and reduces course correction, that pointing an agent at existing file patterns helps it anchor on real conventions, and that running one agent to write code while a second verifies it via review and tests is a recommended two-person-style workflow — and cites OpenAI's Codex documentation as recommending an [[DefinedTerm/agents-md]] file to give an agent consistent expectations about tests, lint rules, dependency policies, and documentation requirements.
- Argues that merge conflicts from parallel agents touching adjacent code are a boundary failure rather than a tooling failure, and recommends [[DefinedTerm/git-worktrees]] together with explicit rules: one agent owns one pull request with no mega-PRs assembled from several agents, the task split is redesigned if two agents might touch the same files, and shared interfaces are handled in a first, human-led pull request that agents then build on top of.
- Argues that as building gets cheap, "should we build this?" starts to matter more than "can we?", and recommends borrowing WIP limits (capping how many active agent streams run at once) and kill criteria (predefined conditions for stopping a feature before it is built) from management practice.
- Describes the author's own current setup as running four to five background agents on low-to-medium complexity work while staying human-in-the-loop across another three to five local sessions for architecture and product nuance, and proposes a repeatable loop for orchestration: plan like a manager, spawn like an orchestrator, monitor async, verify aggressively, integrate carefully, and retro by updating [[DefinedTerm/agents-md]] and checklists.

## Context

The post explicitly cautions that not everyone needs ten to fifteen agents running at once, presenting Boris Cherny's workflow as an extreme that shows what's possible rather than a requirement. It links to the author's own separate writing on orchestration becoming mainstream and lists three of his later posts as related reading. It closes by pointing readers to the author's O'Reilly book, [[Book/beyond-vibe-coding]], for a fuller treatment of AI-assisted and agentic engineering.
