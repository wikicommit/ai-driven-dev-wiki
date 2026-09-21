---
title: "Taming Agents in the Mercari Web Monorepo"
type: "schema:BlogPosting"
lang: en
tags: [agents, agent-config, monorepo, frontend]
sources:
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20251030-taming-agents-in-the-mercari-web-monorepo/'
    hash: sha256:2be25eae3259d1a99d5bcb659f731c2564ffe64e94c6bf0ad803148e7fb2a464
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An account of Mercari's Web team consolidating divergent per-tool agent rule files into a single AGENTS.md acting as an entrypoint to smaller topical documents, with a workflow that has an agent propose edits to those rules from a pull request's changeset."
  author: ["Maximilien Mellen"]
  datePublished: "2025-10-30"
  publisher: "[[Organization/mercari]]"
---

This post describes a coordination problem and the file the team used to solve it. Mercari's Web team, building the company's new Global App, is made up of people from diverse backgrounds whose tools and setups differ widely, and the post states the goal as enabling engineers to use AI tooling without forcing them into a completely different setup. Its stated position is that the answer to divergent tooling was not to make everyone use the same tool — the AI landscape being described as continuing to evolve quickly — but to find a way to align different work styles toward a shared goal.

The problem it names is agents without shared context. Cursor, [[SoftwareApplication/claude-code]], GitHub Copilot and latterly Codex CLI were all in use; users of the first two wrote rules in the format each tool expected, work was duplicated among the maintainers of those rules, and no process kept them in sync, so the rule sets slowly diverged. Engineers who used less popular tools, the post says, often had to open every prompting session with the same corrections and reminders. Its summary of the situation is that familiarity with diverse tools grew while productivity with any one of them did not scale well.

[[DefinedTerm/agents-md]] is presented as what resolved this: a tool-agnostic configuration standard the team adopted as a single source of truth, with `CLAUDE.md` and other rule files becoming symlinks to it. The post's closing framing is that the file became more than a shared rulebook — a bridge between people, tools and ideas — letting every engineer keep their own setup while moving in the same direction.

## Key Points

- The team's rules had diverged because each tool wanted its own format: Cursor and Claude Code rules were maintained separately, the work was duplicated across maintainers, and there was no process to keep them in sync.
- The author's own starting point was an incrementally grown `CLAUDE.md` — after each agentic session, asking Claude to summarize what it judged worth remembering for a future session and appending that to the file. The post says this worked for the author without yet bringing the team much value.
- The team adopted the standard the post first found as `AGENT.md`, singular, described as an RFC proposed by Sourcegraph through its AmpCode project, and consolidated its existing Cursor and Claude rules into one such file. The post records that the rest of the team was still wondering about that RFC's longevity at the time.
- The file became plural after OpenAI secured the agents.md domain, which the post describes as the only thing that had been holding the standard back from the plural wording — and which was also the filename OpenAI's own Codex had already been using. The post credits OpenAI's backing with the standard gaining much more traction among the tools the team used, Cursor not least, and the team then adopted the pluralized form as its single source of truth.
- The file is an entrypoint rather than the rules themselves: the version shown is a short `AGENTS.md` whose sections each point at a separate document under `docs/` — build and test commands, code style and standards, project architecture, authentication patterns, and testing strategy.
- The architecture document is singled out as crucial given the repository's modular approach; the post's stated consequence of omitting that context is that most tools' output ends up having to be completely restructured by the developer unless the same initial context is carefully prompted every time. The excerpt shown records pnpm workspaces with module types `@app/*`, `@feature/*`, `@domain/*` and `@core/*`, a dependency flow of core → domain → feature → app enforced by `eslint-plugin-boundaries`, and what each architectural layer holds.
- Design-system rules are taught to agents explicitly, the post's stated reason being that the project must follow its design system and cannot rely on vibe-coded CSS. The excerpt uses emphatic ALWAYS/NEVER directives — always import components from the internal design system package rather than from source files, never add inline styles on a design system component or native HTML element, and use the design system's color tokens and Panda CSS utilities for custom styling.
- The team's documentation-maintenance workflow is to run an agent against a pull request's changeset together with the rules folder, for any pull request with significant impact on higher-level design, and have the model itself suggest edits to the rules or point out inconsistencies in the code. The post's stated reason for automating this is that editing a non-local markdown file in a separate folder is often tedious for an engineer focused on a task. It calls the result automatically self-enforcing and self-updating documentation.
- What the team was working on at the time of writing was an agent to run on every pull request, automatically flagging code that diverges from these rules whether written by a human or a machine — with the stated aims of detecting bad AI output, training new members faster, and letting a senior engineer making a deliberate structural change automatically generate a patch to the relevant rules.
- The post reports no measurement. Its claims about onboarding engineers faster and reducing prompt boilerplate are the team's own account of its experience.

## Context

The post positions the work inside Mercari's adoption of AI-Native development principles, and states the reason for the tool-agnostic approach directly: everyone was empowered to adopt tools of their choosing and given resources to try new technology, which let the team learn about a broad range of tools quickly while the efficacy of those tools and the shape of their output varied greatly, even within teams.

Its account of the standard's history is written from the position of an adopter rather than a participant — what the team found, when the naming changed, and what that did to the traction of the tools it cared about. The post refers to a colleague's earlier article on the monorepo's architecture and to the AmpCode announcement about the naming, but describes neither beyond the role each plays in its own narrative.

The author's stated aim at the end is to share these learnings across Mercari and to inspire other teams exploring AI-Native development, with the goal given as letting humans and agents work side by side.
