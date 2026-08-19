---
title: "GitHub Agentic Workflows"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-coding, automation, ci-cd]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/automate-repository-tasks-with-github-agentic-workflows/'
    hash: sha256:a7e67b197abef24e12573910d68177edbc8c8fc9c5f039cefe2a57a5de27832a
  - type: url
    url: 'https://docs.github.com/en/copilot/concepts/agents/about-github-agentic-workflows'
    hash: sha256:49ae0743978d367e3e6eb74444e5c4a76951e09d3460bb9315bc2e76dd795e2d
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "AI-powered repository automations authored as Markdown files with YAML frontmatter, compiled to a hardened GitHub Actions lock file and executed by a coding agent. Workflows run read-only by default, with write operations confined to declared \"safe outputs\"."
  applicationCategory: "Repository automation with coding agents"
  author: "GitHub"
---

GitHub Agentic Workflows are AI-powered repository automations that a developer defines in Markdown and runs as GitHub Actions workflows. GitHub's documentation draws the contrast against conventional automation directly: "Unlike traditional automation with fixed if-then rules, agentic workflows use coding agents to understand context, make decisions, and take meaningful actions—all from natural language instructions" — while the guardrails, such as triggers, permissions and safe outputs, are still declared explicitly in frontmatter. The announcement post's summary of the same idea is that "you describe the outcomes you want in plain Markdown, add this as an automated workflow to your repository, and it executes using a coding agent in GitHub Actions."

The feature originated at GitHub Next, which describes starting it as an investigation into a single question: "what does repository automation with strong guardrails look like in the era of AI coding agents?" GitHub Actions was chosen as the substrate because, in GitHub's account, that is where it already provides permissions, logging, auditing, sandboxed execution and rich repository context — and because building on Actions makes coding agents available across millions of repositories while leaving the decision of when and where to use them with the repository owner.

## Overview

Each workflow is one Markdown file in two parts: YAML frontmatter between `---` markers configuring when the workflow runs, what permissions it has and which write operations are allowed; and a Markdown body carrying the natural-language instructions the agent follows. The announcement post puts the division as "The Markdown is the intent, but the trigger, permissions, tools, and allowed outputs are spelled out up front."

The lifecycle adds a compilation step that distinguishes this from prompting an agent directly. The author writes the `.md` file, compiles it into a hardened `.lock.yml` GitHub Actions workflow file, commits and pushes both to the default branch, and then runs it like any other Actions workflow — on a trigger, from the GitHub web interface, or from the GitHub CLI. Compilation is done with the `gh aw` CLI extension (`gh extension install github/gh-aw`, then `gh aw compile`), and GitHub's own recommendation is to generate the workflow with an interactive coding agent rather than writing it by hand, reviewing and validating the result before adding it to the repository.

The tasks GitHub lists for it are repository chores rather than build pipeline work: triaging and labelling incoming issues, investigating CI failures and suggesting fixes, generating daily or weekly status reports, keeping documentation aligned with code changes, and improving test coverage. The announcement post groups the same material into six "continuous" categories — triage, documentation, code simplification, test improvement, quality hygiene and reporting — and names the resulting practice [[DefinedTerm/continuous-ai]].

GitHub is explicit that this is not a CI/CD replacement: agentic workflows "are designed to augment existing CI/CD rather than replace it", do not replace build, test or release pipelines, and their use cases largely do not overlap with deterministic CI/CD workflows.

## Features

Both sources here are GitHub describing its own product; the guardrails below are as GitHub's documentation states them, not independently verified.

- **Engine choice.** Multiple coding agents are supported, specified in the frontmatter `engine` property, each requiring its own authentication secret. The documentation names GitHub Copilot, Anthropic Claude, OpenAI Codex and Google Gemini, with [[SoftwareApplication/github-copilot]] as the default if none is specified; the announcement post names Copilot CLI, Claude Code and OpenAI Codex as examples.
- **Read-only by default.** Workflows have read-only repository permissions unless more is explicitly granted.
- **Safe outputs.** Write operations — creating issues, adding comments, opening pull requests — are only allowed through validated `safe-outputs` declared in the frontmatter, which map to pre-approved, reviewable GitHub operations.
- **Threat detection.** Proposed outputs are scanned for suspicious or unsafe changes before write actions are applied.
- **Isolation.** Agents run in firewalled, sandboxed GitHub Actions environments with tool allowlisting and network isolation, and secrets are kept in isolated downstream jobs rather than exposed to the agent runtime.
- **Role-based access.** Who can trigger or modify agentic workflows can be restricted through role-based access controls.
- **Cost controls.** Inference is metered in AI Credits, with `1 AIC = $0.01 USD`; `gh aw logs` and `gh aw audit RUN-ID` report duration, token usage and AIC estimates, and `max-ai-credits` in frontmatter caps a single run, defaulting to 1,000 AIC. GitHub notes the AIC values are best-effort estimates that may not match provider invoices. Total cost has two parts — GitHub Actions minutes plus inference — with Copilot-engine usage mapping to Copilot billing and third-party engines billed by their provider.

GitHub's stated reason for this architecture is a comparison with the obvious alternative: running a coding agent CLI directly inside a standard Actions YAML workflow, which it says "often grants these agents more permission than is required for a specific task", where agentic workflows instead give read-only access by default and route GitHub operations through safe outputs for "tighter constraints, clearer review points, and stronger overall control." It describes the whole design as defense-in-depth against unintended behaviours and prompt-injection attacks — see [[DefinedTerm/indirect-prompt-injection]].

## History

GitHub announced the feature in [[BlogPosting/automate-repository-tasks-with-github-agentic-workflows]] on 13 February 2026, describing it as available in technical preview and as "a collaboration between GitHub, Microsoft Research, and Azure Core Upstream"; the documentation describes it as in public preview and subject to change. Both are GitHub's own characterisations and the two documents use different words for the stage.

GitHub's guidance for teams at that point was a shift in emphasis rather than a technique: workflows "work best when you focus on goals and desired outputs rather than perfect prompts", with the author providing clarity on what success looks like and letting the workflow explore how to achieve it. It notes workflows can range from very general ("Improve the software") to very specific, and offers as a rule of thumb that "if repetitive work in a repository can be described in words, it might be a good fit for an agentic workflow." Requirements at preview were GitHub Actions enabled on the repository, an account with an AI engine, and the GitHub CLI installed and authenticated.
