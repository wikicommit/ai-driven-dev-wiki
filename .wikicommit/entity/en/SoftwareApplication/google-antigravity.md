---
title: "Google Antigravity"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-coding, ide, ai-assisted-programming]
sources:
  - type: url
    url: 'https://antigravity.google/blog/introducing-google-antigravity'
    hash: sha256:225ceaf15b2f7d9bdf516bd157b93cadb57a94ac3a9cbcd4464971a5cf516212
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An agentic development platform announced by Google in November 2025. Its core is an AI-powered IDE experience built on Google's models, extended with browser control, asynchronous interaction patterns, and an agent-first product form factor intended to let agents autonomously plan and execute end-to-end software tasks."
  applicationCategory: "Agentic development platform"
  author: "Google"
  operatingSystem: "MacOS, Linux, Windows"
---

Google Antigravity is an agentic development platform announced by Google on 18 November 2025 in [[BlogPosting/introducing-google-antigravity]]. Its core is described as a familiar AI-powered IDE experience built on Google's models, which the announcement positions as evolving the IDE toward an agent-first future through browser control capabilities, asynchronous interaction patterns, and an agent-first product form factor — together intended to let agents autonomously plan and execute complex, end-to-end software tasks.

The announcement frames the product as a response to a specific claim about model capability: that with Gemini 3, models had reached a point of running for longer periods without intervention across multiple surfaces, so the surface enabling communication between agent and user should itself look and feel different. Google states its goal for Antigravity is to be "the home base for software development in the era of agents."

## Overview

Antigravity exposes two primary surfaces. The **Editor view** is a conventional AI-powered IDE experience with Tab completions, in-line Commands, and an agent in the side panel, for working synchronously with an agent. The **Manager surface** is agent-first and inverts that arrangement — rather than embedding an agent within a surface, it embeds surfaces into the agent. Google describes it as a mission control for spawning, orchestrating, and observing multiple agents across multiple workspaces in parallel. The two are deliberately kept in separate windows, with the design optimized for instantaneous handoffs between them rather than for combining both experiences in one view.

## Features

Google describes Antigravity as bringing together four tenets of collaborative development:

- **Trust** — agentic work is presented at a task-level abstraction rather than as either a raw stream of every tool call or a final diff with no context. As the agent works it produces **Artifacts**: tangible deliverables such as task lists, implementation plans, walkthroughs, screenshots, and browser recordings, which are easier for a user to validate than raw tool calls.
- **Autonomy** — agents can operate across editor, terminal, and browser simultaneously, with the Manager surface exposing that autonomy for asynchronous interaction.
- **Feedback** — Antigravity starts with local operation and allows asynchronous user feedback on every surface and Artifact, including Google-doc-style comments on text Artifacts and select-and-comment feedback on screenshots. Feedback is incorporated into the agent's execution without requiring the user to stop the agent's process.
- **Self-improvement** — learning is treated as a core primitive, with agent actions both retrieving from and contributing to a knowledge base. Google says this can cover explicit information such as code snippets or derived architecture as well as more abstract material such as the series of steps taken to complete a subtask; knowledge items are viewable from the Agent Manager.

## History

Antigravity was introduced on 18 November 2025 as a public preview, available for individuals at no charge with what Google describes as generous rate limits on Gemini 3 Pro usage. The preview is compatible with MacOS, Linux, and Windows, and offers model optionality within the agent: access to Google's Gemini 3, Anthropic's Claude Sonnet 4.5 models, and OpenAI's GPT-OSS. Google states that rate limits refresh every five hours and are correlated with the amount of work done by the agent rather than with a fixed prompt count, and that its modeling suggests only a very small fraction of power users will ever reach the per-five-hour limit.
