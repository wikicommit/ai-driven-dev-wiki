---
title: "Agents CLI in Agent Platform: create to production in one CLI"
type: "schema:BlogPosting"
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
  description: "Google's announcement of Agents CLI in Agent Platform, a command-line tool built to be driven by AI coding agents. It argues that the main obstacle to shipping agents is a fragmented cloud toolchain that costs coding assistants time and tokens in documentation, and offers a machine-readable interface across the lifecycle instead."
  author: "Ivan Cheung, Pier Paolo Ippolito, Elia Secchi"
  publisher: "[[Organization/google]]"
  datePublished: "2026-04-22"
---

The post announces [[SoftwareApplication/agents-cli]] and frames the problem it addresses as tooling rather than model capability: AI agents are moving from experimental scripts to production services, but the infrastructure for building, evaluating and deploying them stays fragmented. Its specific complaint is about what that fragmentation costs a coding assistant — isolation from the cloud environment, and time and tokens spent ingesting large volumes of documentation just to bridge the gap between local and cloud.

Its proposal is a command-line tool designed for AI coding agents to drive rather than for a person to type, giving them what the post calls a direct, machine-readable line to the full Google Cloud agent stack. Running one setup command injects bundled skills into the coding environment, which the post describes as supplying assistants the exact references they need to scaffold standard-compliant projects immediately. The worked illustration is a natural-language prompt to a coding agent — an expense agent that auto-approves under $50 and requires human approval above it — which the assistant turns into a scaffolded project.

The post is explicit that this is not meant to remove the developer. Alongside the agent-driven path it describes a Human Mode in which the same commands are run directly in a terminal or a script for deterministic execution, which it presents as stepping in to guide the "hands and eyes" of the AI whenever wanted.

## Key Points

- The stated obstacle is a fragmented toolchain rather than model capability: developers and their coding assistants struggle with isolation and waste time and tokens ingesting documentation to bridge local and cloud.
- The tool is positioned as the unified programmatic backbone for the Agent Development Lifecycle on Google Cloud, covering Agent Platform, Cloud Run and agent-to-agent integration.
- It is aimed specifically at AI coding agents, naming Gemini CLI, Claude Code and Cursor as examples.
- Bundled skills are injected into the coding environment by a single command, which the post says gives assistants the API references needed to scaffold functional, standard-compliant projects.
- The lifecycle it covers runs from scaffolding through evaluation to deployment: creating a project, running evaluations against ground-truth datasets, comparing trajectory scoring across runs, provisioning infrastructure, deploying, and registering the deployed agent for distribution.
- Deployment automation is described as injecting infrastructure as code, setting up CI/CD pipelines, and deploying to Agent Runtime, Cloud Run or GKE.
- Both an agent-optimized mode and a Human Mode are supported, the latter for deterministic execution of the same commands directly.
- The post's claims about speed — from idea to production "in hours, not weeks", against a rhetorical figure of 70 days for going from prototype to a secure globally distributed service — are its own positioning, not measured results.

## Context

The post is a product announcement published on Google's developer blog by members of the team behind the tool, so its framing of the problem and its assessment of the solution come from the same party. Its closing call is to download the tool, read the documentation and join the community, and it situates the release within a broader "Agentic Internet" framing.
