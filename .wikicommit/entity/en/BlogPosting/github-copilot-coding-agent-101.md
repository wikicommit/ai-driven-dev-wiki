---
title: "GitHub Copilot coding agent 101: Getting started with agentic workflows on GitHub"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agent-tooling]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/github-copilot-coding-agent-101-getting-started-with-agentic-workflows-on-github/'
    hash: sha256:6144c6b7e4fe07bdc9dd325f45c74f73d95f372935d7794b280556efd97c4585
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A GitHub blog introduction to Copilot coding agent — an asynchronous agent that takes an assigned task, works in a GitHub Actions environment and delivers a draft pull request — covering how to hand it work, its security controls, how it differs from agent mode, and extending it with MCP."
  author: ["Alexandra Lietzke"]
  datePublished: "2025-09-11"
  publisher: "[[Organization/github]]"
---

An introductory post on GitHub's blog, published on September 11, 2025 and updated on January 14,
2026, on [[SoftwareApplication/github-copilot-coding-agent]]. It describes the agent as a software
engineering agent that runs independently in the background to complete assigned tasks, similar to a
peer developer: handed a task, it spins up a customizable development environment powered by GitHub
Actions and can be tracked from issue to pull request to review and approval.

The post's framing is that the agent takes on tedious, low-to-medium complexity work — fixing bugs,
implementing incremental features, refactoring, improving test coverage, updating documentation — so
that developers can focus on the work that interests them, while remaining in control through
pull-request review.

## Key Points

- Tasks can be handed to the agent by assigning a GitHub issue to Copilot on github.com or GitHub
  Mobile, by delegating from Visual Studio Code through the GitHub Pull Requests extension, or from the
  agents panel on github.com; it can also be prompted from Copilot Chat in an IDE or from any
  MCP-supported tool.
- Once handed a task, the agent opens a draft pull request tagged `[WIP]` that it uses to track its
  work, pushes commits as it goes, and logs key steps; when done, it updates the pull request's title
  and description and tags the developer for review.
- Feedback is given by leaving comments that tag `@copilot` on the pull request, which the agent uses
  to iterate.
- To do its work, it reviews the repository's context, including related issues, pull request
  discussions and custom instructions.
- It runs in a sandboxed, ephemeral environment on GitHub Actions with restricted internet access and
  limited repository permissions, and that environment can be customized with the tools and
  dependencies a project needs.
- Its built-in protections, as the post lists them: it can only push to branches it creates (such as
  `copilot/*`); it cannot approve or merge its own pull requests; CI/CD checks in GitHub Actions do not
  run without human approval; its commits are co-authored for traceability; and existing
  organization policies and branch protections apply automatically.
- Against a traditional IDE assistant, where the developer still creates the branch, writes commit
  messages, opens the pull request and manages reviews, the coding agent works inside the GitHub pull
  request workflow and automates those steps, with every step logged and visible to the team.
- The post distinguishes it from agent mode: the coding agent is an asynchronous collaborator running
  in GitHub Actions, whereas agent mode pairs with the developer synchronously inside an IDE such as VS
  Code, JetBrains, Eclipse or Xcode.
- It ships with the Playwright and GitHub MCP servers built in, and repository administrators can add
  others through a JSON configuration in the repository settings; its internet access is limited by a
  firewall whose default rules allow the hosts it needs to interact with GitHub and download
  dependencies.

## Context

The post is GitHub's own introductory material for its product, written by a GitHub content writer;
its descriptions of what the agent does well are the vendor's claims rather than evaluated results.
It follows GitHub's earlier announcement of the agent,
[[BlogPosting/github-copilot-meet-the-new-coding-agent]].
