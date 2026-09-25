---
title: "GitHub Copilot CLI"
type: "schema:SoftwareApplication"
lang: en
aliases: ["Copilot CLI"]
tags: [coding-agents, coding-tools]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.01418'
    hash: sha256:bbc1053e3b6e6a0aa7c93d9962cf8cb956ef31b8a516dbcb70bf3743e8cbf04d
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/agent-driven-development-in-copilot-applied-science/'
    hash: sha256:900fe932178827ecd6df3b0cd594d93c22c0e9cd960bd539ec89b97b0a9e6ed3
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/from-one-off-prompts-to-workflows-how-to-use-custom-agents-in-github-copilot-cli/'
    hash: sha256:908a068edfb3a08239ae4b7a9d0277e7b0d0f94b1ed81916e9b85d32d72e5c33
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "GitHub's agentic command-line tool, in which an agent calling large language models executes semi-autonomous commands on the user's behalf from the terminal."
  applicationCategory: "Agentic command-line coding tool"
  author: "[[Organization/github]]"
---

GitHub Copilot CLI is an agentic command-line tool from [[Organization/github]]. Tools of this kind,
as [[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]] describes them, harness
agents that call large language models and execute semi-autonomous commands on the user's behalf from
the command line; that paper groups it with [[SoftwareApplication/claude-code]] and
[[SoftwareApplication/gemini-cli]] as agentic command-line tools growing in popularity among software
developers. It is distinct from the non-CLI forms of [[SoftwareApplication/github-copilot]] — code
completion, chat and agent mode in IDEs such as VS Code.

## Capabilities

A GitHub researcher's account of building an internal agent tool with it
([[BlogPosting/agent-driven-development-in-copilot-applied-science]]) shows the interaction modes
it exposes: a `/plan` command for working out a feature with the agent before any change is made,
and an `/autopilot` mode in which the agent implements the agreed plan. From inside a session the
agent can also be prompted to request a review from [[SoftwareApplication/github-copilot-code-review]],
wait for it, address the relevant comments and re-request review until none remain. The same post
describes the Copilot SDK as powered by Copilot CLI, giving agents built on it access to existing
tools and MCP servers and a way to register new tools and skills.

It also runs [[DefinedTerm/github-copilot-custom-agents]]. GitHub's post on the feature
([[BlogPosting/custom-agents-in-github-copilot-cli]]) describes adding an agent profile — a Markdown
file ending in `.agent.md`, with YAML frontmatter defining the agent's role, scope, capabilities and
guardrails — to a repository's `.github/agents` directory, and selecting the agent from Copilot CLI
with the `/agent` slash command. That post calls Copilot CLI well suited to agent-driven work because it
already runs scripts, calls APIs and works directly with repositories, so a team can encode an
execution-heavy workflow once — a security audit, an infrastructure-as-code compliance review, release
notes, an incident first look — and run it the same way each time from the terminal.

## Adoption & Ecosystem

The most detailed account of its adoption comes from the study of [[Organization/microsoft]]'s
early-2026 internal rollout, where Copilot CLI was one of two sanctioned agentic command-line tools
alongside Claude Code; Microsoft had access through a product preview program before general
availability. Among engineers eligible to adopt it, first use spread mainly through social exposure —
engineers whose skip-level peers or managers already used it were markedly more likely to try it —
while engineers who had leaned on IDE Copilot before the rollout were more likely to try Copilot CLI
but less likely to keep using it.

In the same study's within-person comparison of single-tool users, weeks with Copilot CLI use showed a
+24.9% lift in merged pull requests against +11.4% for Claude Code. The authors offer two hypotheses:
that engineers used the two tools for different task mixes, and that because Microsoft owns GitHub,
organisational forces likely helped align the Copilot CLI harness with how Microsoft engineers work.
Shortly after the study window closed, an internal announcement indicated that most Microsoft
engineers' Claude Code licenses would be discontinued, with affected engineers directed to Copilot
CLI; some surveyed developers reported migrating toward it.
