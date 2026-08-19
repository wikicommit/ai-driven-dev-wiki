---
title: "Introducing Codex"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, ai-assisted-programming]
sources:
  - type: url
    url: 'https://openai.com/index/introducing-codex/'
    hash: sha256:c899f94e6c00781777e4a0c930a154bee0271654282a1a6f195b368868a1366b
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "OpenAI's launch post of 16 May 2025 announcing Codex as a research preview: a cloud-based software engineering agent powered by codex-1 that runs each task in an isolated sandbox. OpenAI has since marked the post as outdated."
  datePublished: "2025-05-16"
  publisher: "[[Organization/openai]]"
---

"Introducing Codex" is [[Organization/openai]]'s launch post of 16 May 2025, tagged Release and Product, announcing [[SoftwareApplication/codex]] as a research preview — "a cloud-based software engineering agent that can work on many tasks in parallel, powered by codex-1." The post is now prefaced with a notice that it is outdated, pointing readers to the current Codex product page and to ChatGPT Work; it also carries an update dated 3 June 2025 recording that Codex had become available to ChatGPT Plus users and that users could now give Codex internet access during task execution.

## Key Points

- **What it does.** Writing features, answering questions about a codebase, fixing bugs, and proposing pull requests for review, with each task running in its own cloud sandbox environment preloaded with the user's repository.
- **The model.** `codex-1`, described as a version of OpenAI o3 optimized for software engineering, trained with reinforcement learning on real-world coding tasks across a variety of environments to produce code mirroring human style and pull-request preferences, follow instructions precisely, and iteratively run tests until they pass.
- **The interaction model.** Access through the ChatGPT sidebar, with **Code** to assign a task and **Ask** to ask a question about the codebase. Each task is processed independently in an isolated environment where the agent reads and edits files and runs commands including test harnesses, linters and type checkers, typically taking between 1 and 30 minutes, with progress observable in real time.
- **Verifiability as a design goal.** On completion the agent commits its changes in its own environment and provides "verifiable evidence of its actions through citations of terminal logs and test outputs", so each step can be traced. The post states that users can check the work through citations, terminal logs and test results, and that when uncertain or facing test failures the agent explicitly communicates the problem — while insisting it "remains essential for users to manually review and validate all agent-generated code before integration and execution".
- **Repository guidance via [[DefinedTerm/agents-md]].** These are described as text files "akin to README.md" telling Codex how to navigate the codebase, which commands to run for testing, and how to follow the project's standard practices; the post adds that, like human developers, Codex agents "perform best when provided with configured dev environments, reliable testing setups, and clear documentation", while claiming `codex-1` performs strongly on evaluations even without them.
- **Sandboxing.** The agent operated entirely within a secure, isolated cloud container with internet access disabled during execution, limited to code provided via GitHub repositories and dependencies pre-installed by a user setup script, with no access to external websites, APIs or services.
- **Abuse prevention.** OpenAI states Codex was trained to identify and precisely refuse requests aimed at developing malicious software while supporting legitimate work, explicitly acknowledging the tension with beneficial uses such as low-level kernel engineering, and says it published an addendum to the o3 System Card reflecting these evaluations.
- **Early use inside OpenAI.** The post reports Codex being used most often by OpenAI engineers to offload repetitive, well-scoped tasks — refactoring, renaming, writing tests — and also for scaffolding features, wiring components, fixing bugs and drafting documentation, with teams triaging on-call issues, planning tasks at the start of the day and offloading background work.
- **Availability and pricing at launch.** Rolling out to ChatGPT Pro, Enterprise and Business users globally with Plus and Edu coming soon; generous access at no additional cost initially, then rate-limited access with on-demand purchase. `codex-mini-latest` was priced at $1.50 per 1M input tokens and $6 per 1M output tokens on the Responses API, with a 75% prompt caching discount.
- **Stated limitations.** No image inputs for frontend work, no ability to course-correct the agent mid-task, and the observation that delegating to a remote agent takes longer than interactive editing.

## Context

The post also announced changes to [[SoftwareApplication/codex-cli]], which OpenAI says it had launched the previous month as a lightweight open-source coding agent running in the terminal: a smaller version of `codex-1` derived from o4-mini, available as the CLI's default model and in the API as `codex-mini-latest`, plus ChatGPT-account sign-in replacing manual API token configuration, and time-limited free API credits for Plus and Pro users.

Its forward-looking section is a prediction rather than a report, and reads as such. OpenAI writes that pairing with AI tools "has quickly become an industry norm", but that it believes "the asynchronous, multi-agent workflow introduced by Codex in ChatGPT will become the de facto way engineers produce high-quality code" — and that the two modes, real-time pairing and task delegation, will ultimately converge into one workflow across IDEs and everyday tools. The named roadmap items are mid-task guidance, collaboration on implementation strategies, proactive progress updates, and assigning tasks from Codex CLI, ChatGPT Desktop, an issue tracker or a CI system. It closes by noting that OpenAI is collaborating with partners to understand the implications of widespread agent adoption for developer workflows and skill development.

An appendix publishes the `codex-1` system message, which OpenAI offers so developers can understand the model's default behaviour and tailor it — giving as an example that the system message encourages Codex to run all tests mentioned in the AGENTS.md file, which a user short on time can ask it to skip.
