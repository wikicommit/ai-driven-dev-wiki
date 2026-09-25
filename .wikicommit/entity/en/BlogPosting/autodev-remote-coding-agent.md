---
title: "AutoDev Remote 编程智能体：你何必只让 AI 在白天分析需求、设计方案"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agent-tooling, sandboxing, mcp, open-source]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/autodev-remote-agent/'
    hash: sha256:5aa003cf8a64acc7d7d2469af5832b29570bcf56fcc09c3cc621d0b345d5a7b9
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A June 2025 Chinese-language blog post by Phodal Huang introducing AutoDev Remote Agent, an open-source part of AutoDev Workbench that runs in GitHub Actions or as an MCP service to analyse issues, plan tasks and write code, and explaining why the author chose a remote agent over building an IDE."
  author: ["Phodal Huang"]
  datePublished: "2025-06-13"
---

This post, written in Chinese by Phodal Huang, announces that AutoDev Remote Agent — part of AutoDev
Workbench and one component of the next stage of [[SoftwareApplication/unit-mesh-auto-dev]] — had entered a
trial phase. The post lists what it can be used for: running as an MCP service on a server, helping analyse
GitHub issues and plan tasks, being integrated into a development process, and writing code, designing
architecture and writing test cases, with automated coding, testing and deployment (limited to GitHub Pages)
named as future goals. Its code is published in the `unit-mesh/autodev-workbench` GitHub repository, and readers
are invited to test it by opening issues there.

The title's question — why let AI analyse requirements and design solutions only during the day — frames remote
agents as assistants that complete development tasks in the background, a direction the author says tools such
as [[SoftwareApplication/claude-code]] and the Codex agent are also pursuing.

## Key Points

- The author explains why AutoDev is not building its own IDE: from earlier work building an IDE on IntelliJ
  Community he concluded that an individual cannot bear the machine and cloud-server costs of an independent
  IDE, and he says he could not accept VS Code's syntax analysis and refactoring capabilities.
- He characterises mainstream AI coding in 2024 as an RPC/Go-plus-Rust agent backend, a WebView front end for
  cross-platform IDEs, and vector-based code indexing and retrieval, and argues that in 2025, with Grep/Ripgrep
  search becoming the preferred alternative to vectorization — which he says is no longer important — and coding
  models such as Claude able to code agentically, agents can run on the server to write, test and deploy code.
- The prototype, built over the preceding month or more, can be used in a GitHub project's Actions to analyse issues, plan
  tasks and write code; the post links it to a GitHub Marketplace action.
- The author says the first version of the agent's design was produced with the help of Augment, which he calls
  the strongest AI coding assistant to date, building on a core refactored out of AutoDev's VS Code version and
  on AutoDev Workbench's assistant design.
- The agent's tool design follows AutoDev Sketch's, adding GitHub tools on top of MCP-wrapped general tools so
  that it can fetch issues and write analysis and planning results back to them; an example run shows 18 tools
  loaded with DeepSeek as the model provider.
- A "Round" mechanism, which the author says Augment created during the design, limits the number of rounds of
  conversation to avoid infinite loops, with each round making tool calls and summarising them, ending in a
  complete task plan.
- The post compares the agent's tools with those of Claude Code, Augment, Cursor Agent and Codex Agent across
  file operations, terminal execution, process management, code search, code analysis, GitHub integration,
  network functions, Jupyter support, memory management and visualisation; in that comparison only AutoDev Remote
  Agent is marked as having GitHub integration. The author acknowledges that the tools still have many bugs.
- For safety when running in GitHub Actions, the author describes sandboxing by creating a complete code-running
  environment inside a GitHub Action and by dynamically creating new GitHub Actions; he says Docker was set aside
  for now because it performed poorly on his old MacBook.
- Next-stage goals named in the post are making AutoDev Remote Agent bootstrap itself and adding process-related
  tools.

## Context

The post is an announcement of the author's own open-source project, and its tool comparison is the author's own
table rather than an independent evaluation.
