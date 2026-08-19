---
title: "Kiro"
type: "schema:SoftwareApplication"
lang: en
tags: [spec-driven-development, agentic-coding, ide]
sources:
  - type: url
    url: 'https://kiro.dev/blog/introducing-kiro/'
    hash: sha256:83f496f2e0d7f844907485218708133937302b71468f8cc11cabc239a5753da9
  - type: url
    url: 'https://aws.amazon.com/blogs/industries/from-spec-to-production-a-three-week-drug-discovery-agent-using-kiro/'
    hash: sha256:88a7c9517554f4f93af74e1fddd0380527eccaa4427916af91e6ffd946845cff
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An agentic IDE announced in July 2025, built on Code OSS and organised around two features — specs, which expand a single prompt into requirements, design, and sequenced tasks, and hooks, which run agents on file events."
  applicationCategory: "Agentic AI IDE"
  operatingSystem: "Mac, Windows, Linux"
---

Kiro is an AI IDE announced in July 2025, presented as a way to work with AI agents from concept through to production. Its announcement, [[BlogPosting/introducing-kiro]], positions it as good at [[DefinedTerm/vibe-coding]] but aimed past it: its stated strength is getting prototypes into production systems, through two features named as central — **specs** and **hooks**.

The framing problem the announcement sets out is what prompt-driven development leaves behind. An application built by prompting repeatedly works, but the assumptions the model made are undocumented, requirements stay fuzzy, and the system's design is hard to reconstruct — which makes it hard to tell whether the application meets its requirements or how the design will affect performance and environment.

## Overview

The announcement describes Kiro's spec workflow as a three-step sequence. From a single prompt such as *"Add a review system for products"*, Kiro is described as generating user stories covering the relevant cases, each with acceptance criteria written in EARS (Easy Approach to Requirements Syntax) notation, on the stated rationale of making the prompt's assumptions explicit. It then, per the announcement, produces a design document by analysing the codebase together with the approved requirements — data flow diagrams, TypeScript interfaces, database schemas, and API endpoints — and finally generates tasks and sub-tasks, sequences them by dependency, and links each back to a requirement, with details such as unit tests, integration tests, loading states, mobile responsiveness, and accessibility attached to individual tasks.

The announcement further states that tasks are triggered one at a time with a progress indicator, that completed work can be audited through code diffs and agent execution history, and that specs stay synced with an evolving codebase: developers can write code and ask Kiro to update the specs, or edit specs manually to refresh the tasks — offered as a fix for the common pattern where the original artifacts stop being updated during implementation. All of these are the product team's own claims; no independent verification is available in the source.

## Features

- **Specs** — requirements, design, and task artifacts generated from a prompt and kept in sync with the codebase. See [[DefinedTerm/spec-driven-development]].
- **Hooks** — event-driven automations that trigger an agent in the background on file save, create, or delete, or on manual trigger. Kiro takes a plain-language prompt, generates an optimised system prompt from it, and selects which repository folders to monitor; the announcement states that once a hook is committed to Git it enforces the standard across the whole team. See [[DefinedTerm/agent-hooks]].
- **Model Context Protocol support** for connecting specialised tools.
- **Steering rules** to guide AI behaviour across a project.
- **Agentic chat** for ad-hoc tasks, with file, URL, and docs context providers.
- **Built on Code OSS**, so existing VS Code settings and Open VSX compatible plugins carry over.

### A reported project using it

[[BlogPosting/three-week-drug-discovery-agent-using-kiro]] is a dated account from an AWS team of building a production agent with Kiro, and it names the artifacts the announcement describes in more concrete terms. Each feature's specification is three files created in order and reviewed before the next: `requirements.md` for feature requirements, acceptance criteria and success metrics, `design.md` for technical architecture, implementation approach and integration points, and `tasks.md` breaking the design into steps "granular enough for autonomous execution while maintaining context about the broader feature". That post also calls Kiro "the first AI coding tool built around specification driven (spec-driven) development", a claim it makes as the vendor.

Steering is described there as three project-wide documents the team wrote — a `product` document defining purpose and key capabilities, a `structure` document enforcing organizational principles such as tool abstraction patterns and error handling standards, and a `tech` document specifying the stack and development guidelines — added automatically as context, and distinguished from specifications by scope: steering covers the whole project, a specification one feature. Hooks are described in use rather than in principle: they listened for file system events and ran predefined prompts in the background to keep `README.md` current as code changed, and because hooks live at repository level the whole team got the automation on checkout.

The same post names two capabilities as future direction rather than as used in that project. **Kiro Powers** are described as specialized expertise modules that load context and tools on demand, addressing what the post calls "the context overload problem of traditional MCP servers" by bundling MCP tools, steering files and hooks with domain best practices and activating only when relevant, with one-click installation instead of MCP configuration. A **Kiro Autonomous Agent** is described as a frontier agent intended to handle software development work as an asynchronous teammate, able to learn from agents already built in the Kiro IDE and reuse those patterns without constant human guidance.

## History

Kiro was announced on 14 July 2025 by Nikhil Swaminathan (Product Lead) and Deepak Singh (VP DevEx & Agents). At announcement it was free during preview with some limits and gated behind a waitlist, supporting Mac, Windows, and Linux and most popular programming languages. The announcement describes a broader roadmap — design alignment across teams, resolving conflicting requirements, eliminating tech debt, rigor in code review, and preserving institutional knowledge when senior engineers leave — as the direction the team is working toward rather than as shipped capability.
