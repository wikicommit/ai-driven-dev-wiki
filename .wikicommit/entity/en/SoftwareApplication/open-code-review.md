---
title: "Open Code Review"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, agent-tooling, cli, review-rules]
sources:
  - type: url
    url: 'https://github.com/alibaba/open-code-review'
    hash: sha256:b9e25b582bd7eea6db72fdab8f395f2c2a3a3d52275e5bb2239736035a7c6c88
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source AI code review CLI, invoked as `ocr`, that originated as Alibaba Group's internal review assistant. Its stated design combines deterministic engineering for the steps that must not go wrong — file selection, bundling, rule matching, comment positioning — with an LLM agent for dynamic decisions and context retrieval."
  applicationCategory: "Code review tool"
  operatingSystem: "Windows, macOS, Linux"
  featureList: "Diff review across workspace, branch range or commit; full-file scan; delegation mode; configurable LLM providers; MCP server support; CI/CD integration; session viewer"
  author: "[[Organization/alibaba]]"
---

Open Code Review is an AI-powered code review CLI, invoked as `ocr`. Its README states that it
originated as Alibaba Group's internal official AI code review assistant, that it served tens of
thousands of developers and identified millions of code defects over two years, and that it was
subsequently open-sourced for the community. It is published under the Apache-2.0 license.

Its operation is described as reading Git diffs and sending changed files to a configurable LLM
through an agent with tool-use capabilities, which produces structured review comments with
line-level precision. The agent can read full file contents, search the codebase and inspect other
changed files for context. Alongside diff review, an `ocr scan` mode reviews whole files, which the
README offers for auditing unfamiliar codebases or directories with no meaningful diff.

The design argument the README makes is against relying on a general-purpose agent for this task.
It names three problems it attributes to that approach — agents cutting corners on larger
changesets and reviewing only some files, reported issues drifting off the actual code location,
and review quality fluctuating with minor prompt variations — and diagnoses the cause as a purely
language-driven architecture lacking hard constraints on the review process. These are the
project's own characterizations of the alternative.

## Capabilities

The stated response to that diagnosis is a split the README calls Deterministic Engineering ×
Agent Hybrid. Engineering logic rather than the model handles four things: deciding exactly which
files need review and which to filter out; bundling related files into one review unit, each run as
a sub-agent with isolated context, which it presents as a divide-and-conquer strategy that stays
stable on large changesets and supports concurrent review; matching review rules to each file's
characteristics through a template engine rather than language-driven guidance; and independent
comment-positioning and comment-reflection modules for location and content accuracy. The agent's
role is confined to dynamic decisions and dynamic context retrieval, with prompt templates and a
toolset the README says were tuned for code review — the toolset from analysis of tool-call traces
in large-scale production data, including call frequency distributions and per-tool repetition
rates.

Installation is through npm as `@alibaba-group/open-code-review`, after which `ocr` is available
globally; an install script, GitHub Release binaries and a from-source build are also documented.
Git 2.41 or later is required, since the tool relies on Git for diff generation, code search and
repository operations. Configuration is interactive — `ocr config provider` and `ocr config model`
walk through provider selection, API key entry and model choice, then test connectivity.

Review can be scoped several ways: `ocr review` covers staged, unstaged and untracked changes;
`--from`/`--to` reviews a branch's changes since it diverged, using merge-base; `--commit` takes a
single commit; and an interrupted range, commit or scan review can be resumed with `--resume` and a
session ID. Results can be written to a file with `--format json --output`, which the README
recommends for AI host agents.

A delegation mode inverts the arrangement: `ocr delegate` has the user's own coding agent perform
the review with its own LLM, while Open Code Review handles file selection and rule resolution, so
no LLM configuration or API key of its own is required.

## Adoption & Ecosystem

The project publishes plugins for several coding agents — the README names Claude Code, Codex,
Cursor, Kimi Code, OpenCode and QCA Forward — plus a portable agent skill for skill-compatible
agents, so that the review can be invoked as a slash command or skill from inside another tool. It
documents an MCP server for extending the review agent with external tools, CI integration for
GitHub Actions, GitLab CI, GitFlic CI and Gerrit, OpenTelemetry-based telemetry, and a browser
session viewer for replaying reviews and marking comments as fixed or ignored.

For evaluation the project publishes [[Dataset/aacr-bench]] and reports results against it. Its
stated finding is that Open Code Review achieves significantly higher precision and F1 than a
general-purpose agent using the same underlying model, while consuming roughly one ninth of the
tokens and completing reviews faster, with lower recall as a deliberate trade-off favouring
precision over noise. This is the project's own benchmark and its own reported result on it; the
README names Claude Code as the general-purpose agent compared against, and the numbers themselves
are given in an image rather than in the text.

Placed against [[DefinedTerm/agentic-code-review]], the project is an argument about where the
agency in an agentic review should sit — not in the loop as a whole, but in the parts of it that
benefit from judgment, with the rest held in place by ordinary code.
