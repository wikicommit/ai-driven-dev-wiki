---
title: "Год с Claude Code: главное — не он сам, а то, что в .claude/"
type: "schema:BlogPosting"
lang: en
tags: [claude-code, practitioner-report, agent-configuration]
sources:
  - type: url
    url: 'https://habr.com/ru/articles/1042408/'
    hash: sha256:c60b8325646056c7f0ec17119edf53b1216097738e16003b09c633aff670fd6b
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A Russian-language Habr retrospective by a backend Python developer on roughly a year of using Claude Code on every task, arguing that the tool's value comes less from the tool itself than from the rules, hooks, skills and slash commands kept in the project's .claude/ directory."
  author: ["opium"]
---

This post, published in the "sandbox" section of Habr, is a first-person retrospective by a developer working on a Python backend in a small team, who says Claude Code became their default tool in March 2025 and who has used it for about a year "to the maximum" — on every task, with [[DefinedTerm/claude-md]] files, hooks, skills, slash commands and two MCP servers tuned to it. The author rejects both "AI killed programming" and "AI = x10 productivity" as empty framings.

The post sorts experience into where the tool helped, where it fell short, and lessons learned late, then sets out what the author calls the main point of the article: that [[SoftwareApplication/claude-code]] out of the box is a decent but unremarkable tool, and that what makes it productive is the contents of `.claude/` — rules, hooks, skills and slash commands. It closes by inviting readers to share their own configurations.

## Key Points

- Bulk routine edits are reported as the clearest win: describe the change in a paragraph, ask for a plan first, review the plan, then let the agent produce a pull request with tests. For large edits the author asks for a plan only, with no code, because rejecting a wrong plan costs a minute while untangling wrong code costs an hour (the author's own practice).
- Reading an unfamiliar repository goes from half a day to about a minute, but the author always checks the summary against a couple of the named files: roughly one summary in five embellishes, describing a function or behaviour that is not in the code (the author's estimate).
- Of ten generated tests, about eight are fine and two are redundant or mock what should not be mocked, by the author's count.
- General architecture questions produce an average answer; the author concluded this was a problem with how the question was posed, and now supplies load characteristics, the existing stack, project history and who will maintain the result before asking.
- Concurrency, retries and eventual consistency are called the model's blind spot: it writes code that looks right but hides the problem, ordinary single-threaded tests do not catch it, and the model often defends its code after being shown the flaw. The author's rule is to have the model list every failure scenario in prose before any code is written.
- In sessions longer than about an hour the model drifts from project conventions (using `requests` instead of `httpx`, `print` instead of the project logger); the author's remedy is a CLAUDE.md and not staying in one session all day.
- A new session has no memory of the previous day, so context should be given explicitly in the first message; numbers the model states (endpoint counts, file sizes) should be verified with a shell command.
- The author calls [[DefinedTerm/model-context-protocol]] servers the most underrated feature, using ones connected to Telegram and GitLab.
- The CLAUDE.md is kept at two levels: a global file with personal habits (language, code style, git rules, safety rules) and a project file with the stack, conventions and things to avoid.
- A single PostToolUse hook that runs the bot's test suite after every edit to a Python file under the project's `bot/` directory — about twenty lines — is called the cheapest high-value setup: on failure Claude sees the error through stderr and tries to fix it (see [[DefinedTerm/agent-hooks]]).
- The author describes [[DefinedTerm/agent-skills]] as packaged expertise — instructions, examples and extra files loaded only when a task falls into their area — and credits the `frontend-design` skill, whose instructions explicitly forbid generic "AI-generated aesthetics", with ending the generic "AI look" of generated frontends.
- Slash commands in the workflow include `/simplify` after any new code and `/security-review` before merges touching payments or personal data.
- Before risky merges the author cross-checks changes with OpenAI's Codex, on the principle that two models trained differently converge on the same error less often than one; the author originally did this with a home-made `/ask-codex` skill, and says OpenAI later released an official plugin for Claude Code that does the same thing more correctly. The pre-commit sequence is `/simplify`, then the Codex cross-check, then `/security-review`, reported to take 5–7 minutes and used only for payments, data migrations and authorization (compare [[DefinedTerm/cross-model-review]]).
- The author argues that people who use Claude Code as an ordinary autocomplete get value worth the cheaper plan, and that most of the savings come from adapting the process around it with project rules, hooks, skills, slash commands and MCP.

## Context

Everything in the post rests on one developer's experience on a Python backend, and the figures it gives (hours saved, the share of embellished summaries or poor tests) are the author's own estimates rather than measurements. The author frames the cross-check with Codex as a principle independent of particular vendors: not trusting a single model on critical code.
