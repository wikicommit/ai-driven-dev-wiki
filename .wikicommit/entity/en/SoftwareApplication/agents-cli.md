---
title: "Agents CLI"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-tooling, deployment]
sources:
  - type: url
    url: 'https://developers.googleblog.com/agents-cli-in-agent-platform-create-to-production-in-one-cli/'
    hash: sha256:3e885a3a1f0cd7d3569bd0492c6f94334876f6d2ff073e6d5514b7c77d7deffa
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A command-line tool for the agent development lifecycle on Google Cloud, built to be driven by an AI coding assistant as well as typed by a person. It covers scaffolding, evaluation, infrastructure provisioning, deployment and publishing through one interface."
  applicationCategory: "Agent development CLI"
  featureList: "Project scaffolding with deployment targets; bundled skills injected into a coding environment; evaluation runs against ground-truth datasets and run-to-run comparison; infrastructure provisioning; deployment to Agent Runtime, Cloud Run or GKE; publishing to Gemini Enterprise; agent-driven and human-driven modes"
  author: "[[Organization/google]]"
---

Agents CLI is a command-line tool covering the agent development lifecycle on Google Cloud, presented as a single programmatic interface across Agent Platform, Cloud Run and agent-to-agent integration. What distinguishes it from a conventional CLI is its intended operator: it is described as designed specifically for AI coding agents, with Gemini CLI, Claude Code and Cursor named as examples, and its purpose framed as giving such an assistant a direct, machine-readable line to the cloud stack instead of leaving it to infer how the pieces fit together from documentation.

The reasoning given for that design is about context cost. When a coding assistant has to guess how disparate cloud components combine, the result is described as endless loops and wasted tokens; the tool's answer is to inject bundled skills into the coding environment with a single setup command, supplying the API references needed to scaffold a standard-compliant project directly.

## Capabilities

- Installed and set up through `uvx google-agents-cli setup`, which injects its bundled skills into the coding environment.
- Scaffolds a project with a chosen deployment target, with automatic defaults available for unattended use.
- Runs evaluation harnesses against ground-truth datasets, and compares trajectory scoring and metrics between two runs.
- Provisions production infrastructure, injecting infrastructure as code and setting up CI/CD pipelines.
- Deploys to Agent Runtime, Cloud Run or GKE, and registers a deployed agent with Gemini Enterprise for distribution.
- Offers two modes over the same commands: an Agent Mode optimized for consumption by a coding assistant, and a Human Mode in which a developer runs the commands directly in a terminal or script for deterministic execution.

## Adoption & Ecosystem

The tool sits on top of the [[SoftwareApplication/gemini-enterprise-agent-platform]] stack rather than replacing it, and its publishing step targets Gemini Enterprise as the distribution point. Its design is an instance of a broader pattern in which tooling is shaped for an AI assistant to operate rather than only for a person — here through skills bundled with the CLI itself, so that the knowledge needed to drive it travels with the tool. The account summarized here is the announcement from its own team, so it establishes the tool's scope and command surface rather than any independent experience of using it.
