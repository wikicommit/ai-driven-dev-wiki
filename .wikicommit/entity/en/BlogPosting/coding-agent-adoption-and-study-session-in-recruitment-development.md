---
title: "人材紹介開発におけるコーディングエージェントの導入状況や勉強会の様子"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, security, team-practices]
sources:
  - type: url
    url: 'https://tech.bm-sms.co.jp/entry/2026/04/28/110000'
    hash: sha256:38fb55e78a639c3dacc43c35d84472e9d170ef9be7e7531356608206999c0168
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A firsthand account from SMS Co., Ltd.'s recruitment-services development group of how its engineers use coding agents, built around an internal AI coding study session that framed harness engineering as the foundation for using agents safely and gave security extended coverage, centred on keeping secrets out of an agent's view."
  author: "熊谷"
  datePublished: "2026-04-28"
  publisher: "SMS Co., Ltd. (エス・エム・エス)"
---

Written by an engineer in the recruitment-services development group at SMS Co., Ltd. (エス・エム・エス), this post describes how coding agents are used day to day in that group and reports on an internal AI coding study session held on 13 March 2026. Its stated premise is that using AI is no longer the open question; what matters now is using it safely and reproducibly.

The company places no restriction on which agent or how much of it engineers use: each person applies for the services they need, and new services go through prior application and review. The author names their own setup — mainly [[SoftwareApplication/openai-codex]], linked locally with [[SoftwareApplication/claude-code]], with [[SoftwareApplication/github-copilot]] reviewing pull requests — and mentions colleagues using [[SoftwareApplication/cursor]], or [[SoftwareApplication/opencode]] combined with a particular LLM.

The study session deliberately avoided "AI is amazing" material in favour of the groundwork for getting that performance out in practice, which the slides presented as an entry point to [[DefinedTerm/harness-engineering]]. Security was covered in some depth, centred on secret handling and organized around one principle: design so that an agent never sees secrets in the first place, rather than trying to stop them after they leak.

## Key Points

- In a survey of the 19 attendees at the start of the session, 63% said they used coding agents in nearly all of their work and 36.8% in part of it; no respondent reported not using them. The most common uses were bouncing design ideas off the agent and writing code, and Claude Code and GitHub Copilot were the most-used tools.
- The session presented harness engineering as operational design for using AI safely and stably, not as making the model itself smarter, on the view that current coding agents are used together with surrounding mechanisms such as [[DefinedTerm/agents-md]], [[DefinedTerm/agent-skills]], [[DefinedTerm/model-context-protocol]] and CLIs.
- AGENTS.md is described as the place for the premises an agent should know first in a repository — facts that change its next action (which package manager is used, that generated files are not edited directly, that schema changes need a migration) rather than values or sentiments.
- Skills are characterized as reusable judgment for a specific task, which the author personally considers a very important element of using coding agents well. MCP is described as convenient but liable to heavy token consumption because the agent reads the server's published specification before deciding how to use it, which the post cites as the reason for a growing tendency to prefer an official CLI where one exists.
- The secret-handling guidance given at the session: do not assume a plaintext `.env` file in the repository; keep secrets in 1Password, which the company already uses for sharing them, and inject them from outside at runtime via a CLI, which the session tried hands-on; separate the agent's development environment from the execution environment in which humans handle secrets, a setup the author considers a good fit for devcontainers; and detect secrets deterministically before commit, with lefthook and secretlint named as tools.
- The session also shared operating rules for extensions: do not casually install unofficial MCP servers or Skills, prefer official or trusted ones, and route uncertain cases through internal review.
- The author's comparison of models — Opus 4.6 taking initiative on its own, GPT-5.4 doing exactly what it is told — is offered explicitly as personal and biased preference rather than an evaluation.

## Context

The post is a company engineering-blog piece with a recruiting purpose, and says so in its closing lines. It treats the study session as one part of a continuing practice: time deliberately set aside for informal AI discussion, where members bring AI news, tools that worked, failed approaches and problems, plus a dedicated Slack channel, on the stated reasoning that individual effort alone produces uneven results. The author acknowledges that the session did not cover security exhaustively, and notes that some tool information was already out of date by the time the post was written.
