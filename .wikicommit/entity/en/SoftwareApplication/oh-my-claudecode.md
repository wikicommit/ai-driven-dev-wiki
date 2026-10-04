---
title: "Oh My ClaudeCode"
type: "schema:SoftwareApplication"
lang: en
aliases: ["OMC", "oh-my-claudecode"]
tags: [claude-code, multi-agent, orchestration, agent-config]
sources:
  - type: url
    url: 'https://velog.io/@sammy0329/Claude-Code%EB%A5%BC-200-%ED%99%9C%EC%9A%A9%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-spec-kit-Everything-Claude-Code-Oh-My-ClaudeCode-%EC%99%84%EB%B2%BD-%EA%B0%80%EC%9D%B4%EB%93%9C'
    hash: sha256:72acff284adbf85c43f84d89f0d728dc7b8061e0e89dd2aac0bbb415897290e6
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An open-source Claude Code plugin that orchestrates multiple agents automatically from natural-language requests, so that the user does not have to learn agents, skills or hooks."
  applicationCategory: "Claude Code plugin for multi-agent orchestration"
  featureList: "Execution modes autopilot, ultrapilot, swarm, pipeline and ecomode; magic keywords; skill layering; 12 agent definitions; 8 hook modules; model routing by task complexity; HUD statusline; evidence-based verification"
---

Oh My ClaudeCode (OMC) is an open-source plugin for [[SoftwareApplication/claude-code]] whose approach is to have the system orchestrate agents automatically, rather than handing the user tools and guidance to apply. Its tagline is "Don't learn Claude Code. Just use OMC.": the user is not meant to learn concepts such as agents, skills and hooks, and the functions a request needs are activated from the natural-language request alone.

A February 2026 Korean guide to three Claude Code add-ons sets OMC beside [[SoftwareApplication/github-spec-kit]] and [[SoftwareApplication/everything-claude-code]], contrasting Everything Claude Code's approach — provide tools and guidance and leave the judgment to the user — with OMC's, in which the system makes the judgment.

## Capabilities

The features the project lists are zero configuration with intelligent defaults, a natural-language interface with no commands to memorise, automatic parallelisation of complex work, persistent execution that does not give up until a task is complete, cost optimisation through model routing (described as saving 30–50%), and automatic extraction and reuse of problem-solving patterns.

- **Execution modes.** Five modes are triggered by a prefix or phrase: *autopilot* for fully autonomous execution of a single complex task; *ultrapilot*, a parallel autopilot with up to five concurrent workers, described as three to five times faster, for multi-component systems; *swarm*, in which N agents share a task pool and claim work atomically, for independent parallel work; *pipeline*, which processes sequential stages and passes data between them, for dependent work; and *ecomode*, a token-saving mode with budget management aimed at cost-sensitive users.
- **Magic keywords.** Besides the mode names, keywords such as `ralph` (do not stop until the work is complete), `ultrawork` / `ulw` (maximum parallel execution), `plan` (start a planning interview) and `tdd` steer a request.
- **Skill layering.** Instead of switching modes, OMC injects skills into a fixed master session to change its behaviour, following the formula `[Execution Skill] + [0-N Enhancement Skills] + [Optional Guarantee]` — for example a default execution skill with `frontend-ui-ux` and `git-master` enhancement skills layered on. Because behaviours are stacked rather than swapped, the guide argues, context is not broken.
- **Agents and hooks.** The source tree holds 12 agent definitions — among them architect, explore, researcher, executor, designer, writer, vision, critic, analyst, orchestrator, planner and a qa-tester that tests CLIs and services through tmux — and 8 hook modules, including a magic-keyword detector, a "ralph loop" self-referential work loop, a todo-continuation hook that enforces task completion, and edit-error recovery.
- **Model routing.** OMC analyses task complexity and selects a model automatically: Haiku for simple work such as documentation updates, Sonnet for feature implementation and code review, and Opus for architectural decisions and complex debugging.
- **Visibility and verification.** A HUD statusline shows the orchestration state in real time, and a verification module requires evidence of completion across build, test, lint, functionality, an architect-level review, completed todos and no unresolved errors.

## Adoption & Ecosystem

OMC is installed from its GitHub repository through Claude Code's plugin marketplace, followed by a setup command that updates `CLAUDE.md`, after which requests are made in natural language. The guide recommends it for fast prototyping, large parallel jobs and cost-sensitive use, rates its learning curve as the lowest of the three tools it compares, and names opacity of the automation as its limitation, to be mitigated by monitoring progress through the HUD. It also suggests combining OMC with Everything Claude Code's rules files, copied into the user's rules directory, to add quality guardrails to OMC's automation.
