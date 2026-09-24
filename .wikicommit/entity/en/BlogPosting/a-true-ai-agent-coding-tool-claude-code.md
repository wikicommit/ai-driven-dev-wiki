---
title: "진짜 AI 에이전트형 코딩 툴 ＇Claude-Code＇"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, coding-tools, model-context-protocol]
sources:
  - type: url
    url: 'https://devocean.sk.com/blog/techBoardDetail.do?ID=167718&boardType=techBlog'
    hash: sha256:e7b042f7217d59682f0651a011746587c44f2da9610f02a1955247d227dbd979
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Korean-language tutorial on SK Telecom's DEVOCEAN developer blog introducing Claude Code as an agentic coding tool, walking through installation, its working modes and a fully automated FastAPI CRUD build, and collecting best practices and reported productivity case studies."
  author: ["broccoli"]
  datePublished: "2025-08-25"
  publisher: "DEVOCEAN"
---

This post, whose title translates as "A true AI-agent-style coding tool: Claude-Code", is an introductory guide to [[SoftwareApplication/claude-code]] written for Korean developers on DEVOCEAN, the developer community blog operated by SK Telecom. Its framing is a contrast with earlier AI coding tools: where tools such as Copilot and Cursor are described as focused on autocompletion and snippet suggestion, Claude Code is presented as a tool that explores, analyses, edits, commits and pushes across a whole codebase "like an engineer" — what the post calls agentic coding, in which the AI plans, executes and resolves problems on its own rather than only proposing code.

Most of the post is practical. It covers installation and authentication, the tips Claude Code shows on first launch, what the `/init` command does in an empty project directory, the three working modes, connecting an MCP server, and a worked example in which one detailed prompt, run with permission prompts switched off, produces a tested FastAPI CRUD API and pushes it to GitHub. It closes with a best-practice table, a list of MCP servers with their install commands, an example permission allowlist, and reference tables for keyboard shortcuts and slash commands.

## Key Points

- The post defines agentic coding as the AI planning a task, executing it and resolving problems autonomously, and presents this as the distinguishing strength of Claude Code over tools centred on code suggestion.
- It explains that the `/init` slash command analyses a codebase and writes a `CLAUDE.md` file of guidance for future Claude Code sessions. In the author's own trial on an empty directory, the tool found no files, decided the project was in its initial state, and wrote a generic guide to a FastAPI CRUD project covering commands, architecture patterns, database migrations and environment variables.
- It describes three working modes cycled with Shift+Tab: Plan, which explains a plan and waits for approval before acting; Auto Accept, which accepts every proposed action; and Normal, the default, which asks for approval on each action.
- Its worked example builds a prompt meant for unattended execution: split create, read, update and delete into independent units processed in parallel, skip plan-mode approval, commit and push every change to Git, apply "ultra think" before writing each block of code, generate pytest and httpx tests and fix failures automatically, and record progress, errors and next steps in a `PROGRESS.md` file so work can resume after an interruption.
- To let that prompt run without waiting for approvals, the author launched Claude Code with `--dangerously-skip-permissions`, and added a GitHub MCP server with `claude mcp add` so the agent could commit and push. The post reports that the run completed in about ten minutes, with ten of ten tests passing and two commits pushed to a public repository — an outcome from the author's single run.
- The post notes that `--dangerously-skip-permissions` skips most permission requests but that some sensitive operations may still require approval internally, and responds by recommending a pre-configured allowlist of tools and commands; its appendix gives an example with `allow` and `deny` lists.
- Its best-practice section — explore, plan, code and commit; write tests first; iterate against screenshots; headless mode for CI; running several Claude instances in parallel on separate Git worktrees — is presented as guidance for using Claude Code and restates, in Korean, workflow categories it names in English. The post itself warns that the "safe YOLO mode" of running unsupervised should be used only in a container without internet access and never for sensitive work.
- The post claims that developers using Claude Code raised development speed by 150% on average and cut bug rates by 83%, attributing this only to "recent statistics" without naming a source.
- A closing section lists productivity case studies across code review, debugging, documentation, test generation, automation scripts and learning, each with a percentage improvement, and attributes them to linked pages by Anthropic and by third-party users rather than to anything the author measured.

## Context

The post is written from the position of an individual practitioner introducing a tool, not from its vendor, and its practical sections rest on the author's own session transcripts. Its quantitative claims are of a different kind: the headline speed and bug-rate figures carry no named source, and the case-study figures are relayed from other pages, so they describe what those pages report rather than anything the post establishes.

Its conclusion is openly promotional of the tool's prospects — that Claude Code is likely to become an industry-standard AI coding tool alongside GitHub Copilot, and that experiencing the change now secures a developer's future competitiveness — and it presents these as expectations rather than findings.
