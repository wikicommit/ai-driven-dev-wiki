---
title: "Codex"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-coding, ai-assisted-programming]
sources:
  - type: url
    url: 'https://openai.com/index/introducing-codex/'
    hash: sha256:c899f94e6c00781777e4a0c930a154bee0271654282a1a6f195b368868a1366b
  - type: url
    url: 'https://openai.com/codex/'
    hash: sha256:d885d8a80478f4aecb76134aac46d1976013ff1a1cf8ecb1eead450eeac6d72a
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "OpenAI's software engineering agent, launched on 16 May 2025 as a cloud-based agent that runs each task in its own isolated sandbox preloaded with the user's repository. OpenAI now presents it as one agent reachable from ChatGPT, an IDE extension and the terminal."
  applicationCategory: "Agentic AI coding tool"
  author: "[[Organization/openai]]"
---

Codex is [[Organization/openai]]'s software engineering agent. It was launched on 16 May 2025 as a research preview described as "a cloud-based software engineering agent that can work on many tasks in parallel", able to write features, answer questions about a codebase, fix bugs and propose pull requests, with each task running in its own cloud sandbox preloaded with the user's repository. OpenAI's later product page presents Codex as a single agent reachable from three surfaces — Codex in ChatGPT, a Codex IDE extension, and [[SoftwareApplication/codex-cli]] — all connected by the user's ChatGPT account.

The launch model was `codex-1`, described as a version of OpenAI o3 optimized for software engineering and trained with reinforcement learning on real-world coding tasks in a variety of environments, with the stated aims of generating code that mirrors human style and pull-request preferences, adhering precisely to instructions, and iteratively running tests until they pass. OpenAI's own comparison claim is that `codex-1` "consistently produces cleaner patches ready for immediate human review and integration into standard workflows" than o3.

## Overview

In the launch design the agent is assigned work from a sidebar in ChatGPT: a prompt plus **Code** to assign a task, or **Ask** to ask a question about the codebase. Each task is processed independently in a separate isolated environment where the agent can read and edit files and run commands including test harnesses, linters and type checkers; OpenAI puts typical completion at between 1 and 30 minutes depending on complexity, with progress observable in real time. On finishing, the agent commits its changes in its own environment and supplies what OpenAI calls verifiable evidence — citations of terminal logs and test outputs — so each step can be traced, after which the user can review, request revisions, open a GitHub pull request, or pull the changes locally.

Codex reads [[DefinedTerm/agents-md]] files placed in the repository to learn how to navigate the codebase, which commands to run for testing, and how to follow the project's practices. OpenAI's framing of that dependency is an analogy: "Like human developers, Codex agents perform best when provided with configured dev environments, reliable testing setups, and clear documentation." It also states that on coding evaluations and internal benchmarks `codex-1` performs strongly even without AGENTS.md files or custom scaffolding.

Sandboxing at launch was strict. The agent operated entirely within a secure, isolated cloud container with internet access disabled during task execution, limiting it to the code provided via GitHub repositories and the dependencies pre-installed by a user setup script, with no access to external websites, APIs or services. A 3 June 2025 update to the launch post records both the extension of Codex to ChatGPT Plus users and the enabling of internet access during task execution.

## Features

OpenAI's product page states the following capabilities, in its own framing:

- Task completion end to end on work described as ranging from routine pull requests to building features, complex refactors and migrations.
- Multi-agent workflows, with built-in worktrees and cloud environments so agents work in parallel across projects — the claim being that this completes "weeks of work in days".
- [[DefinedTerm/agent-skills]] as the mechanism for teaching Codex a team's standards, workflows and ways of working, applied consistently across tasks so the agent needs less supervision.
- Scheduled, always-on background work such as issue triage, alert monitoring and CI/CD.
- Code review, with the claim that Codex raises baseline quality through more thorough designs, comprehensive testing and high-signal review so issues are caught early.

The launch post is candid about what was missing at the time: image inputs for frontend work, and the ability to course-correct the agent mid-task. It also notes that delegating to a remote agent takes longer than interactive editing, which "can take some getting used to".

## History

Codex launched on 16 May 2025 as a research preview, rolling out to ChatGPT Pro, Enterprise and Business users globally with Plus and Edu support said to be coming soon; the 3 June 2025 update records Plus availability arriving. OpenAI described free generous access for an initial period followed by rate-limited access and on-demand usage pricing.

The launch post also announced CLI-side changes — a smaller version of `codex-1` derived from o4-mini, available as `codex-mini-latest` — which are covered on [[SoftwareApplication/codex-cli]].

The stated direction was convergence. OpenAI wrote that pairing with AI tools had already become an industry norm but predicted that "the asynchronous, multi-agent workflow introduced by Codex in ChatGPT will become the de facto way engineers produce high-quality code", and that real-time pairing and task delegation would ultimately converge into one workflow spanning IDEs and everyday tools. Its named roadmap items were mid-task guidance, collaboration on implementation strategies, proactive progress updates, and assigning tasks from Codex CLI, ChatGPT Desktop or an issue tracker or CI system. OpenAI has since marked the launch post as outdated, pointing readers to the current product page.
