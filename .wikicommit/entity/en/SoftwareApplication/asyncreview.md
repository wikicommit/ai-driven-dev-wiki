---
title: "AsyncReview"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, agent-tooling, sandboxing]
sources:
  - type: url
    url: 'https://github.com/AsyncFuncAI/AsyncReview'
    hash: sha256:fe75d41284e3b16f547100098c199269e82a0d07655fa5e6c55e1989662c322e
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source agentic code review tool for GitHub pull requests and issues. It describes itself as using Recursive Language Models to explore a repository, fetch context and verify findings in a sandbox before answering, rather than reasoning from the diff alone."
  applicationCategory: "Code review tool"
  featureList: "Repository exploration beyond the diff; Python REPL sandbox for verification; GitHub API tool interception; runnable via npx; installable as an agent skill"
---

AsyncReview is an open-source tool that performs agentic code review on GitHub pull requests and
issues. Its self-description is that it uses Recursive Language Models to go beyond simple diff
analysis, autonomously exploring the repository, fetching relevant context, and verifying its
findings in a secure sandbox before answering. Its README states it is inspired by DevinReview.

The loop it documents has five stages: the agent reasons and plans, generates Python code, executes
that code in a Python REPL sandbox alongside model queries and tool commands, has its tool calls —
the README names fetching a file and searching — intercepted and served from the GitHub API, then
observes the result and repeats recursively.

The argument the README makes for this shape is a contrast with tools that read only the changed
lines. It presents four pairings: limited context against reading any file in the repository to
understand dependencies, static analysis that guesses how code works against executing search
queries and verification scripts, inventing library methods against citing existing file paths and
lines, and one-shot generation against iterating before answering. This is the project's own
characterization of the alternatives, not an independent comparison. The README reports no
evaluation or benchmark; the one performance claim it makes is unquantified, its architecture
diagram terminating in a "10x High Quality Answer".

## Capabilities

The tool runs without installation through `npx asyncreview review`, taking a pull request or issue
URL and a free-text question. It requires a Gemini API key, supplied as `GEMINI_API_KEY`; for
private repositories it additionally needs a GitHub token, either as `GITHUB_TOKEN` or through a
`--github-token` flag. The README notes the token can be obtained from the GitHub CLI.

Beyond direct invocation, AsyncReview is designed to be used as a skill by other agentic providers —
the README names Claude, Cursor, OpenCode, Gemini and Codex — on the stated grounds that this lets
them see and reason about codebases they have no local access to. Installation for that path is
`npx skills add AsyncFuncAI/AsyncReview`, which the README says works with agents compatible with
`vercel/skills`; manual setup points the agent at a `skills/asyncreview/SKILL.md` file. A backend
server and web interface can also be run locally, documented separately in the repository.

## Adoption & Ecosystem

The repository is published under the MIT license by the GitHub account AsyncFuncAI. Its file
listing reflects the several entry points described above, with separate `cli`, `npx`, `web` and
`skills/asyncreview` directories.

What the project represents in the wider picture is the skill-packaged form of
[[DefinedTerm/agentic-code-review]] — a reviewer that acts in the repository rather than reading a
diff, offered not only as a tool of its own but as a capability another coding agent installs and
calls.
