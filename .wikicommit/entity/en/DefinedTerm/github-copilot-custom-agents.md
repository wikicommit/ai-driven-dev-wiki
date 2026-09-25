---
title: "Custom agents (GitHub Copilot)"
type: "schema:DefinedTerm"
lang: en
aliases: ["Copilot custom agents", "Agent profile"]
tags: [coding-agents, agent-config]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/from-one-off-prompts-to-workflows-how-to-use-custom-agents-in-github-copilot-cli/'
    hash: sha256:908a068edfb3a08239ae4b7a9d0277e7b0d0f94b1ed81916e9b85d32d72e5c33
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Copilot agents defined by Markdown agent profiles stored in a repository, which specify an agent's role, the tools it may use and the guardrails it follows so that it behaves the same way wherever it runs."
---

In [[SoftwareApplication/github-copilot]], a custom agent is a Copilot agent defined by a Markdown
file — an agent profile — rather than relying on generic behaviour. The profile describes the agent's
role and area of expertise, which tools it can access, the standards and guardrails it must follow and
the outputs it should produce, with the stated result that the agent behaves consistently wherever it
runs. GitHub presents it as a way to make a general coding agent into a specialized one: where a
generic agent might suggest how to clean up code, a custom agent applies a team's own formatting
rules, tooling, accessibility standards, review requirements and safety requirements every time.

## Usage

An agent profile is a Markdown file with YAML frontmatter — fields such as `name`, `description`,
`tools` and, in one of GitHub's examples, `model` — followed by the agent's instructions. In
[[SoftwareApplication/github-copilot-cli]], a profile is added to the `.github/agents` directory of a
repository with a filename ending in `.agent.md`, and the agent is selected with the `/agent` slash
command. Because the profile lives in the repository, GitHub's framing is that a team can review,
version and share it like code, so the same expectations follow the work from the terminal to the IDE
and into pull requests.

GitHub distinguishes custom agents a team writes from off-the-shelf agents built with partners such as
JFrog, Dynatrace, Octopus Deploy and Arm. It recommends the partner agents for trying a working agent
with minimal setup and for tool-specific best practices, and the team's own custom agents where a team
needs its conventions, internal tooling and exact stack followed every time — noting that teams often
start from a partner agent and adapt it. Its examples of workflows suited to the mechanism are security
audits, infrastructure-as-code compliance reviews, release notes and incident first-look reports
([[BlogPosting/custom-agents-in-github-copilot-cli]]).
