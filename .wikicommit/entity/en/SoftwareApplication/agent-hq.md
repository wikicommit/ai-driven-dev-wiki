---
title: "Agent HQ"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, agent-orchestration, governance]
sources:
  - type: url
    url: 'https://github.blog/news-insights/company-news/welcome-home-agents/'
    hash: sha256:3d6ec841322ac0387923d4793d10946b52ad17fdca90ec22708b55bf57feced1
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "GitHub's platform layer for running third-party coding agents natively inside the GitHub flow, combining a cross-surface command center, editor-side planning and customization, and enterprise governance controls."
  applicationCategory: "Agent orchestration platform"
  featureList: "Third-party coding agents under one Copilot subscription; mission control across GitHub, VS Code, mobile and CLI; branch controls and agent identity; Plan Mode and custom agents in VS Code; GitHub MCP Registry; agent control plane; Copilot metrics dashboard"
  author: "[[Organization/github]]"
---

Agent HQ is GitHub's name for making coding agents native to the GitHub flow rather than something
bolted onto it. Announced at GitHub Universe 2025 (see
[[BlogPosting/introducing-agent-hq]]), it is described by GitHub as an open ecosystem that unites
agents from several vendors on one platform, reached through a paid
[[SoftwareApplication/github-copilot]] subscription instead of through each vendor's own surface.
GitHub states that agents from Anthropic, OpenAI, Google, Cognition and xAI would become available
this way over the months following the announcement.

What Agent HQ deliberately leaves unchanged is part of how GitHub defines it: the working
primitives stay Git, pull requests and issues, and the compute stays GitHub Actions or self-hosted
runners. The layer it adds is direction and governance — one place to assign and track agent work,
editor-side controls over how an agent behaves, and administrative controls over which agents may
run at all.

## Capabilities

- **Mission control** — a command center GitHub describes as a consistent interface across
  GitHub, VS Code, mobile and the CLI rather than a single destination. From it a developer can
  pick from a fleet of agents, assign work in parallel, and track progress from any device.
- **Branch controls** giving granular oversight of when CI and other checks run against
  agent-created code.
- **Agent identity**, so that which agent is building a task, its access, and the policies applied
  to it are managed as they would be for a human team member.
- **One-click merge conflict resolution**, improved file navigation, and code-commenting
  improvements.
- **Integrations** with Slack and Linear, alongside previously announced connections for Atlassian
  Jira, Microsoft Teams, Azure Boards and Raycast.
- **Plan Mode in VS Code**, where Copilot asks clarifying questions to build a step-by-step
  approach before implementation; once the plan is approved it is handed to Copilot to implement,
  locally or through a cloud agent.
- **Custom agents configured through [[DefinedTerm/agents-md]] files** — source-controlled
  documents carrying rules and guardrails that shape an agent's behaviour without re-prompting —
  and custom agents in GitHub Copilot with their own system prompt and tools.
- **GitHub MCP Registry in VS Code**, for discovering, installing and enabling
  [[DefinedTerm/model-context-protocol]] servers with a single click. GitHub states that VS Code is
  the only editor supporting the full MCP specification.
- **Agent control plane** — the governance layer for enterprise administrators, covering security
  policies, audit logging, access management, which agents are permitted, and which models they
  may reach. In public preview at announcement.
- **Copilot metrics dashboard**, in public preview at announcement, reporting Copilot usage and
  impact across an organization.

## Adoption & Ecosystem

GitHub positions Agent HQ against a problem it states in terms of code quality rather than
capability: a review can pass — "LGTM" — while the change still degrades the codebase into
long-term technical debt. GitHub Code Quality, announced in public preview alongside Agent HQ,
extends Copilot's security checks to the maintainability and reliability impact of changed code and
adds org-wide visibility and reporting. Separately, a code review step was added inside
[[SoftwareApplication/github-copilot-coding-agent]]'s own workflow so that its output receives a
first-line review before a human sees it.

The first partner agent to arrive was [[SoftwareApplication/openai-codex]], which GitHub made
available to Copilot Pro+ users in VS Code Insiders in the week of the announcement — described as
the first of the partner agents to extend beyond its own native surfaces into the editor.

All of the above is GitHub's own account of a platform it was announcing rather than an independent
report of shipped behaviour, and several capabilities are stated as forthcoming or in public
preview at the time of writing.
