---
title: "Onboarding your AI peer programmer: Setting up GitHub Copilot coding agent for success"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agent-tooling, context-engineering]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/onboarding-your-ai-peer-programmer-setting-up-github-copilot-coding-agent-for-success/'
    hash: sha256:822cf11b61d2b4dee40e368a8a3a65011646e0467d0e94521e2341528f263d3b
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A GitHub blog post that treats setting up GitHub Copilot coding agent like onboarding a new developer: configuring its GitHub Actions environment, writing well-defined issues, keeping the repository well documented, adding custom instructions, extending it with MCP servers and managing its firewall."
  author: ["Christopher Harrison"]
  datePublished: "2025-07-31"
  publisher: "[[Organization/github]]"
---

A post on GitHub's blog, published on July 31, 2025 by a GitHub senior developer advocate, on how to
prepare a repository for [[SoftwareApplication/github-copilot-coding-agent]]. Its organizing analogy is
that much of the setup resembles onboarding a new developer — good documentation and a streamlined
setup process — while a few things are specific to Copilot being an AI.

The post first distinguishes Copilot's two agentic capabilities: coding agent, which it describes as
an autonomous tool that takes an issue, spins up an Actions container, iterates in the background and
returns a pull request, and agent mode, an interactive sidekick in the editor or on github.com that
executes smaller multi-step tasks with the developer in real time. It then follows the coding agent's
workflow step by step and says, for each step, what a team can do to help it produce a better pull
request.

## Key Points

- When assigned an issue, the coding agent follows a set pattern: it creates a branch, creates a pull
  request to track its work, creates a contained environment running inside GitHub Actions, reads the
  issue or prompt, explores the project, works iteratively toward a solution, and finally updates the
  pull request and notifies the team it is ready for review.
- The agent's environment is configured with a workflow file at
  `.github/workflows/copilot-setup-steps.yml` containing a job that must be named
  `copilot-setup-steps`, listing the steps that install whatever the environment needs; the post's
  example sets up Python dependencies and SQLite. The author suggests reusing an existing workflow
  that already creates a development environment.
- The author advises telling Copilot how something should be done rather than leaving it to install
  requisite services on its own, which may lead to unexpected versions or other mistakes.
- The more clearly defined the issue, the better the pull request; the post recommends including a
  clear problem statement or user story, full error output and reproduction steps for bugs, relevant
  history, and suggestions on how to approach the issue, and gives a sample issue for migrating tests
  from unittest to pytest.
- Standard documentation and project-structure practice helps the agent the same way it helps
  developers: when it takes an issue it first explores the codebase, reading README files and
  searching for related code, so an up-to-date README, code comments, good naming and a logical folder
  structure give it a more predictable environment.
- Custom instructions come in two kinds: a repository-wide `.github/copilot-instructions.md` applied to
  all requests, and `<file-name>.instructions.md` files under `.github/instructions/` whose `applyTo`
  glob targets specific files. The post suggests the repository-wide file cover what is being built,
  user stories, frameworks and libraries, project structure and global coding guidelines, and
  recommends targeted instructions files for correcting particular kinds of mistake the agent keeps
  making.
- The agent can use [[DefinedTerm/model-context-protocol]] servers; the GitHub and Playwright MCP
  servers are available by default, an existing `.vscode/mcp.json` in the project can be used to
  identify MCP servers, and otherwise servers are configured in the repository's Copilot coding agent
  settings. The post's example enables the Azure MCP server restricted to Bicep schema support.
- The agent has a default firewall limiting its internet access to core services such as the npm and
  pip package hosts, which the post presents as a way to manage data exfiltration risk should
  malicious instructions reach the agent; adding a remote MCP server or other internet access means
  updating the firewall's allow list.
- The pull request's "View session" button shows everything the agent did, which the author recommends
  both for validating its work and for refining how tasks are assigned and its environment configured.

## Context

This is guidance from a GitHub developer advocate about GitHub's own product, drawn from the author's
experience rather than measured results. The author notes that investing in instructions files also
helps when Copilot is used in the IDE, not only when tasks are assigned to the coding agent.
