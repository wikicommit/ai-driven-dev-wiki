---
title: "GitHub Copilot: Meet the new coding agent"
type: "schema:BlogPosting"
lang: en
tags: [agents, coding-tools, agent-sandboxing]
sources:
  - type: url
    url: 'https://github.blog/news-insights/product-news/github-copilot-meet-the-new-coding-agent/'
    hash: sha256:f3a6917c79f2f70870a12536be1e700c8b33381be9f7cfe35243aba5ec7dab46
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "GitHub's May 2025 announcement of the Copilot coding agent: assign an issue to Copilot and it works in the background on GitHub Actions, pushing commits to a draft pull request."
  author: "Thomas Dohmke"
  datePublished: "2025-05-19"
  publisher: "[[Organization/github]]"
---

This is GitHub's announcement of [[SoftwareApplication/github-copilot-coding-agent]], published in
May 2025 and updated later the same month. Its central claim is an interface one: the way to
delegate work to the agent is to assign a GitHub issue to Copilot, exactly as an issue would be
assigned to a team member, after which the agent works in the background and delivers its output as
a draft pull request.

The post's other emphasis is that delegating to an agent should not require relaxing a repository's
existing controls. It sets out a default policy set — branch restrictions, a bar on the requester
approving the agent's own pull request, a limited internet allowlist, and CI workflows that do not
run without human approval — and presents these as the reason an agent can be added to a team
without weakening its security posture.

## Key Points

- The agent is invoked by assigning one or more GitHub issues to Copilot, from github.com, GitHub
  Mobile or the GitHub CLI; it can also be asked to open a pull request from Copilot Chat on GitHub
  or in VS Code.
- Once assigned, it adds an eyes emoji reaction, then boots a virtual machine, clones the
  repository, configures the environment and analyses the codebase using retrieval augmented
  generation powered by GitHub code search.
- It pushes its changes to a draft pull request as git commits and updates the pull request
  description as it goes, with its reasoning and validation steps visible in session logs.
- GitHub states the agent excels at low-to-medium complexity tasks in well-tested codebases —
  adding features, fixing bugs, extending tests, refactoring, improving documentation — which is a
  scoping claim, not a measured result.
- [[DefinedTerm/model-context-protocol]] servers can be configured in the repository's settings to
  give the agent access to data and capabilities outside GitHub, including GitHub's own MCP server.
- Vision model support lets the agent read images attached to the issues assigned to it, so a bug
  screenshot or a feature mockup can be part of the task.
- After finishing, it tags the requester for review and picks up review comments automatically,
  proposing code changes in response.
- GitHub's stated reason for choosing GitHub Actions as the compute layer is scale: Actions,
  introduced in 2018, is described as the largest CI/CD ecosystem in the world, with more than
  25,000 actions in the GitHub Marketplace and more than 40 million jobs run every weekday.
- Four default policies are applied: the agent may push only to branches it created; the developer
  who asked for the pull request cannot approve it, so existing required-review rules are honored;
  the agent's internet access is limited to a customizable trusted list; and GitHub Actions
  workflows do not run without human approval.
- At announcement the agent was available to Copilot Enterprise and Copilot Pro+ customers, opted
  in per repository, with an additional organization policy for Enterprise. From June 4, 2025 it
  was to consume one premium request per model request.

## Context

The post is GitHub's own product announcement, so its characterizations of the agent's strengths
are the vendor's. It carries two customer quotes supplied for the announcement — a DevEx lead at EY
describing the agent as letting developers assign work that would otherwise detract from deeper
work, and an engineering vice president at Carvana describing it as converting specifications to
production code in minutes — which are relayed by GitHub rather than independently reported.

The agent is presented as the continuation of an internal effort the post calls Project Padawan,
and as one point on a line GitHub draws through its own products: code completions, next edit
suggestions, chat, agent mode, and now a background agent.
