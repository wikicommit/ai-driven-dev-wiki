---
title: "Better Harness"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-tooling, coding-agents, harness-engineering, evaluation, open-source]
sources:
  - type: url
    url: 'https://github.com/QoderAI/better-harness'
    hash: sha256:05fa6b236fc51caec519b58e2aa01157d1f3b832ed5ba7f5316eb7419de99179
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source, MIT-licensed tool from QoderAI that runs through a coding agent, analyses the workflow around the agent's work rather than only its final diff, and turns project and session evidence into prioritized, evidence-bounded findings across the five dimensions of its Agent Work Loop model."
  applicationCategory: "Coding-agent workflow analysis"
  author: "QoderAI"
---

Better Harness is an open-source tool, published by QoderAI under the MIT license, for analysing and
improving the workflow around AI coding agents. Its README summarises the idea as "Delegate coding to
agents. Improve the loop around them": the tool runs through the coding agent a developer already
uses, gathers project evidence (and, on hosts where it is supported, session evidence), and turns it
into prioritized improvements and verifiable next steps. The repository's own description calls it a
[[DefinedTerm/harness-engineering]] platform for coding agents.

The problem it addresses is framed as one that reviewing the final diff cannot see. The README lists
five ways the workflow around an agent goes wrong — fuzzy goals, so that the agent confidently solves
the wrong problem; improvised steps that nobody can reproduce; "it works" claims without proof;
review and delivery checks bypassed for speed; and lessons lost, so the same friction returns on the
next task — and positions Better Harness as analysing those system-level problems instead.

## Capabilities

Better Harness organises its analysis around a feedforward-and-feedback loop, citing Martin Fowler's
site for the framing (see [[DefinedTerm/guides-and-sensors]]): feedforward guides such as `AGENTS.md`,
specs, skills and acceptance criteria steer the agent before it acts, and feedback sensors such as
linters, tests, hooks and evaluation agents observe the results and help it self-correct. Across that
loop it evaluates five dimensions of delivery that it calls the **Agent Work Loop**:

| Dimension | The question it asks |
| --- | --- |
| Task Understanding | Does the agent know the goal and what "done" means? |
| Controlled Execution | Is the work on supported, repeatable paths? |
| Change Validation | Is there evidence the change actually works? |
| Reliable Delivery | Does AI speed bypass quality checks or acceptance? |
| Learning Capture | Does the next task benefit from this one? |

Running the `/better-harness` workflow establishes a task-bounded baseline and produces a report
combining a five-part overview, prioritized findings, the agent assets it detected and an evidence
brief. Each finding is tied to its evidence and carries an impact, an expected output, a scoped repair
and acceptance checks; a repair action drafts a scoped fix plan for review. Depending on the host, the
report is a host-native Canvas (Qoder and Cursor) or a self-contained HTML file with paired Markdown
(Claude Code, Codex, Qwen Code, GitHub Copilot and Kimi Code). Once comparable reports exist over
time, a history view shows how the five dimensions move, which the project presents as recorded trends
rather than causal proof of improvement. A separate interactive Harness Inspector traces delivery from
product intent through agent activity, sessions, files and commits in a read-only workspace.

The project stresses that missing evidence stays explicit. Unobserved behaviour is reported as such
rather than turned into an unsupported score, and the README draws the boundary this way: configured
assets can establish that a mechanism exists, but only linked task evidence can establish that it was
used or improved an outcome. Internally, three independent evidence agents collect from separate
domains, and a single lead agent unifies their results.

What the repository opens is described as three connected layers: engineering-practice guidance
(covering session evidence, project harness, agent customisation and
[[DefinedTerm/loop-engineering]]), the Agent Work Loop evaluation model, and the runnable
implementation — the canonical `/better-harness` workflow packaged as an
[[DefinedTerm/agent-skills]] skill, together with evidence collectors, analysers, renderers and thin
per-host adapters. A standalone CLI can inspect local installation evidence for every host and build
install, update or removal plans for a host without executing them.

## Adoption & Ecosystem

Better Harness does not use one entry point across hosts; it is installed separately per coding agent,
mostly as a plugin through each host's marketplace mechanism. The README gives inline setup for
[[SoftwareApplication/claude-code]], Codex Desktop and the Codex CLI ([[SoftwareApplication/openai-codex]]),
[[SoftwareApplication/qoder]], [[SoftwareApplication/cursor]] and the
[[SoftwareApplication/github-copilot-cli]], and points to its documentation for Qwen Code, Pi, Kimi
Code, WorkBuddy and Grok. It is built into the Qoder desktop app, where it needs no installation and is
also reachable from a sidebar entry in Qoder's Quest view, and a Qoder CLI installed alongside the
desktop app picks it up as well. The Cursor plugin is not published to a marketplace, so the tool
reports its Cursor installation plan as unavailable rather than emitting an unverified command.
Session evidence depends on what each host records — for GitHub Copilot, for instance, it reads Copilot
CLI transcripts, while noting that Copilot records no per-response token usage and that VS Code
Copilot Chat has no supported durable transcript.
