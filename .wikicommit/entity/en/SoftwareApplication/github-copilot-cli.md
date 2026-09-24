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
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "GitHub's agentic command-line tool, in which an agent calling large language models executes semi-autonomous commands on the user's behalf from the terminal; GitHub announced its general availability on February 25, 2026."
  applicationCategory: "Agentic command-line coding tool"
  author: "[[Organization/github]]"
---

GitHub Copilot CLI is an agentic command-line tool from [[Organization/github]]. Tools of this kind,
as [[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]] describes them, harness
agents that call large language models and execute semi-autonomous commands on the user's behalf from
the command line; that paper groups it with [[SoftwareApplication/claude-code]] and
[[SoftwareApplication/gemini-cli]] as agentic command-line tools growing in popularity among software
developers. It is distinct from the non-CLI forms of [[SoftwareApplication/github-copilot]] — code
completion, chat and agent mode in IDEs such as VS Code. GitHub announced its general availability
on February 25, 2026.

## Adoption & Ecosystem

The most detailed account of its adoption comes from that study of [[Organization/microsoft]]'s
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
CLI; some surveyed developers had already reported migrating toward it.
