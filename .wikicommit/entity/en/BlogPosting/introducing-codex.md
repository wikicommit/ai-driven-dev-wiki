---
title: "Introducing Codex"
type: "schema:BlogPosting"
lang: en
tags: [agents, coding-tools, sandboxing]
sources:
  - type: url
    url: 'https://openai.com/index/introducing-codex/'
    hash: sha256:2eb8d6fdb2ff536487274af973fe01fefa7c639f4f5ae546a6739e3e516ba93c
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "OpenAI's May 2025 research-preview announcement of Codex, a cloud-based software engineering agent that works on many tasks in parallel, each in its own isolated sandbox preloaded with the user's repository. The page now carries a notice that the launch post is outdated."
  author: "OpenAI"
  publisher: "OpenAI"
  datePublished: "2025-05-16"
---

*Introducing Codex* is OpenAI's announcement of a research preview of
[[SoftwareApplication/openai-codex]], published on 16 May 2025 and rolled out first to ChatGPT
Pro, Enterprise and Business users. It presents Codex as a cloud-based software engineering agent
that can work on many tasks in parallel — writing features, answering questions about a codebase,
fixing bugs, and proposing pull requests — with each task running in its own cloud sandbox
preloaded with the user's repository.

The post is explicit that this is an early, iterative release rather than a finished product, and
the version of the page read here carries a later notice stating that the launch post is outdated
and pointing readers to the current Codex product pages. A dated update of 3 June 2025 records
that Codex became available to ChatGPT Plus users and that internet access during task execution
was being enabled.

## Key Points

- Codex is powered by codex-1, described as a version of OpenAI o3 optimized for software
  engineering and trained with reinforcement learning on real-world coding tasks so that it
  produces code close to human style and PR preferences, follows instructions precisely, and can
  iterate on tests until they pass.
- Each task is processed independently in an isolated environment where Codex can read and edit
  files and run commands including test harnesses, linters and type checkers, typically taking
  between 1 and 30 minutes.
- Verifiability is presented as a deliberate design choice: Codex cites terminal logs and test
  outputs so each step can be traced, and explicitly communicates uncertainty and test failures.
  OpenAI states it remains essential for users to manually review and validate all
  agent-generated code before integration and execution.
- Codex can be guided by [[DefinedTerm/agents-md]] files in the repository, though OpenAI reports
  codex-1 performing strongly on coding evaluations and internal benchmarks even without them or
  any custom scaffolding.
- At launch the agent ran with internet access disabled, limiting it to the code in the connected
  GitHub repositories and to dependencies pre-installed by a user-supplied setup script. OpenAI
  notes separately that this describes the launch configuration only.
- On abuse, OpenAI states Codex was trained to identify and precisely refuse requests aimed at
  developing malicious software while still supporting legitimate work that uses similar
  techniques, such as low-level kernel engineering, and that it strengthened its policy
  frameworks and safety evaluations to reinforce those boundaries.
- OpenAI reports its own engineers using Codex mainly to offload repetitive, well-scoped tasks —
  refactoring, renaming, writing tests — and names four companies from a small group of external
  testers it worked with before release; those accounts are relayed by OpenAI rather than
  independently reported.
- Based on what it learned from those early testers, OpenAI recommends assigning well-scoped
  tasks to multiple agents simultaneously and experimenting with different task types and
  prompts.
- Alongside the cloud product it announces a smaller version of codex-1, derived from o4-mini,
  as the new default model in Codex CLI and as `codex-mini-latest` in the API, optimized for
  low-latency code Q&A and editing.

## Context

The closing argument is about where the industry is heading rather than about the product: OpenAI
writes that pairing with AI tools has quickly become an industry norm, but predicts the
asynchronous, multi-agent workflow Codex introduces in ChatGPT will become the de facto way
engineers produce high-quality code, with real-time pairing and task delegation eventually
converging into one workflow. It names the limitations it accepts for now — no image inputs for
frontend work, no way to course-correct the agent mid-task, and the latency of delegating to a
remote agent — and says guidance mid-task, collaboration on implementation strategies and
proactive progress updates are planned. That is a vendor's forecast about its own product
category, not an independent assessment.

An appendix publishes the codex-1 system message so that developers can understand the model's
default behaviour, and much of it is the AGENTS.md contract stated as rules the agent follows:
that such a file's scope is the directory tree rooted where it sits, that more deeply nested files
take precedence on conflict, that direct system, developer and user instructions outrank them, and
that any programmatic checks the file specifies must be run after all code changes. The rest
covers git conventions and a citation format for referencing file paths and terminal output in
the final response.
