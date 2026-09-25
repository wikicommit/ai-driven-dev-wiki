---
title: "From one-off prompts to workflows: How to use custom agents in GitHub Copilot CLI"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agent-config, cli]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/from-one-off-prompts-to-workflows-how-to-use-custom-agents-in-github-copilot-cli/'
    hash: sha256:908a068edfb3a08239ae4b7a9d0277e7b0d0f94b1ed81916e9b85d32d72e5c33
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A GitHub blog post explaining how custom agents — Copilot agents defined by Markdown agent profiles kept in a repository — turn repeated terminal tasks in GitHub Copilot CLI into consistent, reviewable workflows, with example profiles and guidance on partner-built versus team-built agents."
  author: ["Jacklyn Carroll"]
  datePublished: "2026-06-09"
  publisher: "[[Organization/github]]"
---

A post on GitHub's blog, dated June 9, 2026, introducing [[DefinedTerm/github-copilot-custom-agents]]
as used from [[SoftwareApplication/github-copilot-cli]]. Its starting point is the friction that
accumulates in the terminal — re-running the same commands, re-explaining context, translating logs
into something a team can act on — and its proposal is to encode a team's context once, in a Markdown
agent profile, so that a repeated task runs the same way every time instead of starting from a
one-off prompt.

Most of the post is four example agent profiles, each a Markdown file with YAML frontmatter naming the
agent, describing it and listing the command-line tools it may use, followed by instructions: a
security-audit agent, an infrastructure-as-code compliance agent, a release-notes agent and an
incident-response agent. It closes with guidance on when to use partner-built agents and when to write
one's own.

## Key Points

- A custom agent is a Copilot agent defined by a Markdown agent profile that describes how it should
  operate, which tools it can use, what standards it follows and what outputs it produces, so that its
  behaviour is consistent wherever it runs.
- In Copilot CLI, a custom agent is created by adding an agent profile — a Markdown file ending in
  `.agent.md`, with YAML frontmatter — to the `.github/agents` directory of the target repository, and
  is invoked with the `/agent` slash command.
- Because the profile is a file in the repository, it can be reviewed, versioned and shared, and the
  post says the same expectations then follow the work from the CLI to the IDE and into pull requests
  on GitHub.
- The post calls Copilot CLI well suited to agent-driven work because it already runs scripts, calls
  APIs and works directly with repositories, so execution-heavy workflows can be encoded once and
  invoked from the terminal.
- Its example profiles share a pattern: a stated goal, operating rules, the checks or commands to run,
  and a fixed output format — for instance a pull-request-ready checklist grouped by severity for the
  security audit, and an approval-ready summary with a risk rating for the infrastructure-as-code review.
- Several of the examples instruct the agent to report a missing tool or unavailable data as a gap
  rather than inventing results, and to redact secrets and credentials from its output.
- GitHub offers off-the-shelf agents built with partners such as JFrog, Dynatrace, Octopus Deploy and
  Arm; the post recommends them for speed and tool-specific best practices, and custom agents when a
  team needs precision, continuity and control over its own conventions and internal tooling.
- Its advice for getting started is to pick a task the team already repeats every week and turn it
  into an agent that runs the same checks with the same tools and produces the same reviewable output.

## Context

The post is GitHub's own product guidance, written by a GitHub content writer, and its claims about
consistency and continuity are the vendor's framing of its feature rather than measured results.
