---
title: "From idea to PR: A guide to GitHub Copilot’s agentic workflows"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agent-tooling]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/from-idea-to-pr-a-guide-to-github-copilots-agentic-workflows/'
    hash: sha256:d26a28f8e99d98794a771d2e9f313c93e3141162781714ff1bfd49653195fa0b
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A GitHub developer-relations walkthrough of turning a feature request into a tested, review-ready pull request with Copilot's issue creation, coding agent, custom chat modes and remote GitHub MCP server."
  author: ["Chris Reddington"]
  datePublished: "2025-07-01"
  publisher: "[[Organization/github]]"
---

A post on GitHub's blog by a developer advocate in GitHub's Developer Relations team, accompanying a
Rubber Duck Thursdays live stream in which the author localized an application — a Next.js web app
and a matching SwiftUI iOS app in separate repositories — into English, French and Spanish. It was
published on July 1, 2025 and updated on August 1, 2025. The post's framing is practical: the
agentic features of [[SoftwareApplication/github-copilot]] are presented as a way to hand off the
boilerplate, refactoring and "pre-work" that stand between a developer and shipping features, while
the developer stays in charge of review and merging.

The walkthrough strings four capabilities into one loop from issue to pull request: drafting the
issue with Copilot, handing it to the [[SoftwareApplication/github-copilot-coding-agent]], a custom
planning chat mode in VS Code, and the remote [[SoftwareApplication/github-mcp-server]].

## Key Points

- The author's stated reason for agentic workflows is the hours teams still spend turning vague
  requests into well-scoped issues, hunting down every file in a cross-cutting refactor, and
  writing the same unit-test scaffolding repeatedly.
- Step one is to describe the request to Copilot on github.com and have it draft a GitHub issue
  with an overview, acceptance criteria and pointers to the files that need changing.
- Assigned that issue, the coding agent creates a branch, starts a session (configuring a
  development environment first if `copilot-setup-steps.yml` is present), explores the codebase
  and forms a plan, uses the repository's custom instructions as context, and opens a draft pull
  request.
- The post insists the pull request be reviewed like any other: read its description and the
  changed files, look at the agent's session to understand its approach, test it in a Codespace or
  through existing CI — and review the code before executing it.
- When the author found hard-coded strings the agent had missed, the fix was a review comment
  asking for them to be localized; the agent picked this up and worked on it in another session.
- Custom chat modes, then in preview in VS Code 1.101, package instructions and allowed tools into
  a `.chatmode.md` file that appears alongside the default Ask, Edit and Agent modes. The author's
  planning mode, adapted from the VS Code team's example, generates an implementation plan without
  editing code and then offers to file it as a GitHub issue; kept in the workspace, the mode is
  shared with teammates through the repository.
- The remote GitHub MCP server is offered as a way to drop the local setup of running MCP servers
  through npm packages or Docker containers, with OAuth 2.0 authentication in place of personal
  access tokens.
- The post distinguishes the coding agent, which works asynchronously on an assigned task, from
  Copilot agent mode, which collaborates synchronously in the editor; it briefly shows an earlier
  agent-mode session in Xcode adding internationalization to the iOS app.
- Its dos and don'ts: keep issues tightly scoped rather than asking the agent to "re-architect the
  app", provide acceptance criteria rather than assume the agent knows the intent, review changes
  carefully before executing code or merging, and iterate rather than expect perfection first time.

## Context

The post is a vendor practitioner's demo account rather than an evaluation: its evidence is one
live-streamed localization task, and its recommendations are the author's own. It closes by calling
agentic workflows tools rather than magic.
