---
title: "Kilo Code"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-agents, coding-tools, open-source, cli]
aliases: ["Kilo"]
sources:
  - type: url
    url: 'https://kilo.ai/open'
    hash: sha256:08d887e0943da16f3ca647b312a8d9418c7b6823fa7c0725b0ea5ff49bfd0e94
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An AI coding agent whose clients for VS Code, JetBrains and the terminal are MIT-licensed open source, with its Gateway and Cloud backend code published as source-available. Its maker describes it as an all-in-one agentic engineering platform that lets users choose among many models."
  applicationCategory: "AI coding agent"
  featureList: "VS Code extension, JetBrains plugin, CLI, Cloud Agents, bring-your-own-key model access"
  author: "Kilo Code, Inc."
---

Kilo Code is an [[DefinedTerm/ai-coding-agent]] made by Kilo Code, Inc. Its local clients — an
extension for VS Code, a plugin for JetBrains IDEs and a command-line interface — are published as
open source under the MIT license, so that users can inspect, modify, fork and run them. The company's
own page on openness pitches this as a way to inspect the coding agent you use and keep your choice of
model. The site carries a banner announcing that Kilo has been acquired by Anaconda.

The company presents Kilo Code as an all-in-one agentic engineering platform rather than a single
point tool, contrasting it with proprietary agents that, in its words, slow users down with gates and
throttles.

## Capabilities

The company's component and license matrix separates what is open source from what is only
source-available:

| Component | Availability | License |
| --- | --- | --- |
| VS Code extension | Open source | MIT |
| JetBrains plugin | Open source | MIT |
| Kilo CLI | Open source | MIT |
| Gateway and Cloud backend | Source available | Repository license |

The Gateway and Cloud backend code is published for inspection, but the security and abuse-protection
code is excluded from it. The page says "open" describes specific code and licenses, not every hosted
service as one undifferentiated package.

As a platform, Kilo Code is described as covering an Architect → Code → Debug → Review flow through
separate architect, code, debug and review agents, without switching applications. The same session
and context are said to carry across VS Code, JetBrains, the CLI and Cloud Agents, so work can start
on a phone, continue on a laptop and be handed to a cloud agent overnight. It supports bringing your
own keys, and the company states that it offers access to more than 500 models from any provider,
switchable at any time.

## Adoption & Ecosystem

The company lists a set of public commitments: features that are open source today stay open source,
bring-your-own-key is always supported, community contributions to the open-source codebase stay
open source, the roadmap is public, and docs, downloads and features can be browsed without an
account. It also says it builds Kilo with Kilo, naming Kilo Autocomplete, Parallel Agents, Kilo
Sessions, Cloud Agents, Code Review, Voice Prompting and a Team AI Dashboard as features shipped in a
six-week span using Kilo Code itself, and that Kilo Deploy went from first commit to general
availability in two weeks — a pace it calls "Kilo Speed". The project invites contributions through
GitHub and has a Discord community.
