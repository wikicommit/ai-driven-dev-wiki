---
title: "Introducing Agent HQ: Any agent, any way you work"
type: "schema:BlogPosting"
lang: en
tags: [agents, coding-tools, agent-orchestration]
sources:
  - type: url
    url: 'https://github.blog/news-insights/company-news/welcome-home-agents/'
    hash: sha256:3d6ec841322ac0387923d4793d10946b52ad17fdca90ec22708b55bf57feced1
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "GitHub's announcement at Universe 2025 of Agent HQ, its plan to make third-party coding agents native to the GitHub flow and to give developers one command center for directing them."
  author: "Kyle Daigle"
  datePublished: "2025-10-28"
  publisher: "[[Organization/github]]"
---

This post is GitHub's own announcement, made at GitHub Universe 2025, of what it calls Agent HQ:
its position that coding agents should not be bolted onto a development platform but made native
to the flow developers already use. The argument it opens with is that the current AI landscape
fragments capability across disconnected tools and interfaces, and that GitHub has historically
addressed problems of this shape — making Git accessible, systematizing code review through pull
requests, automating deployment with Actions.

The concrete commitment is that coding agents from Anthropic, OpenAI, Google, Cognition and xAI
will become available directly within GitHub over the following months, as part of a paid GitHub
Copilot subscription, rather than each being reached through its own surface. Around that sit a
command center for directing them, editor-side features for planning and customizing agent
behaviour, and administrative controls for governing agent access. The post is a product
announcement written in GitHub's own voice, so its claims about the platform's direction are
GitHub's stated intent rather than an independent account of shipped behaviour.

## Key Points

- GitHub states that coding agents from Anthropic, OpenAI, Google, Cognition and xAI will become
  available directly within GitHub as part of a paid Copilot subscription over the months
  following the announcement. This is GitHub's own forward-looking statement about its roadmap.
- What Agent HQ does *not* change is presented as being as important as what it does: the
  primitives stay Git, pull requests and issues, and the compute stays GitHub Actions or
  self-hosted runners.
- Starting the week of the announcement, Copilot Pro+ users could work with
  [[SoftwareApplication/openai-codex]] in VS Code Insiders — described by GitHub as the first
  partner agent to extend beyond its own native surfaces into the editor.
- Mission control is described as a consistent interface across GitHub, VS Code, mobile and the
  CLI rather than a single destination, from which a developer can assign work to several agents
  in parallel and track their progress.
- GitHub frames agent identity as an access-control problem of the same kind as a human
  collaborator's: identity features to control which agent is building a task, with access and
  policies managed as they would be for any other developer on the team.
- Plan Mode, introduced in VS Code alongside the announcement, has Copilot ask clarifying
  questions to build a step-by-step approach before code is written; GitHub's stated rationale is
  that supplying context upfront surfaces gaps, missing decisions and project deficiencies early.
- Custom agents in VS Code are configured through [[DefinedTerm/agents-md]] files, which GitHub
  describes as source-controlled documents carrying rules and guardrails such as "prefer this
  logger" or "use table-driven tests for all handlers", so that behaviour need not be re-prompted
  each time.
- GitHub's stated problem with code review in an agentic setting is that "LGTM" does not always
  mean the code is healthy: a review can pass while still degrading the codebase into long-term
  technical debt. GitHub Code Quality, in public preview at the time, is offered as org-wide
  visibility and reporting against that.
- A code review step was added inside the Copilot coding agent's own workflow, so that
  [[SoftwareApplication/github-copilot-coding-agent]] receives a first-line review and addresses
  problems before a human sees the code.
- The control plane is presented as an agent governance layer for enterprise administrators:
  security policies, audit logging and access management in one place, including which agents are
  permitted and which models they may reach.

## Context

The post is a vendor announcement and reads as one — its closing section argues that AI tooling
has so far meant more context-switching, more babysitting and more subscriptions, and positions
Agent HQ against that. Claims about capability are GitHub's own, and several are stated as
forthcoming rather than available.

Quotes from partner companies are carried in the post as an image caption rather than body prose:
product leads at OpenAI, Anthropic and Google Labs each endorse the integration, with Anthropic's
framing agents as working "alongside your team like any other collaborator". These are supplied by
the partners to GitHub for the announcement, not independent assessments.

The post's framing of a fleet of specialized agents working in parallel, directed from a single
control surface, is the same shape as [[DefinedTerm/factory-model]] and
[[DefinedTerm/conductor-and-orchestrator-modes]], though the post itself does not use those terms.
