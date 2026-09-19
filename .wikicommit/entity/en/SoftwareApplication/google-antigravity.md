---
title: "Google Antigravity"
type: "schema:SoftwareApplication"
lang: en
sources:
  - type: url
    url: 'https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/'
    hash: sha256:702649e8a757da9007eeda56b0fe7deceaa3aa8140675fe480fce240e9ac2760
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [agents, coding-tools, agent-architecture, human-oversight]

properties:
  description: "Google's agentic development platform, combining an AI-powered editor with an agent-first Manager surface; its agents plan, execute and verify tasks across the editor, terminal and browser."
  applicationCategory: "Agentic development platform"
  operatingSystem: "macOS, Windows, Linux"
  featureList: "Editor View with tab completion and inline commands; Manager surface for spawning, orchestrating and observing asynchronous agents; agent Artifacts (task lists, implementation plans, screenshots, browser recordings); inline feedback on Artifacts; knowledge base of saved context and code snippets"
  author: "[[Organization/google]]"
---

Google Antigravity is an agentic development platform published by
[[Organization/google]], announced in November 2025. Google describes it not as an editor
but as a platform that combines a familiar AI-powered coding experience with an
agent-first interface, from which agents can be deployed to autonomously plan, execute
and verify complex tasks across the editor, terminal and browser.

The design premise Google states for it is that agents should have a dedicated space to
work in rather than occupying a sidebar, and that a developer should be able to operate
at a task-oriented level instead of supervising individual edits. Its answer to the
resulting trust problem is to have agents report through reviewable deliverables rather
than through raw tool-call logs.

## Capabilities

The platform presents two distinct surfaces. The Editor View is an AI-powered IDE with
tab completions and inline commands, for the synchronous hands-on workflow Google
describes as already familiar.
The Manager surface is the agent-first interface, where several agents can be spawned,
orchestrated and observed working asynchronously across different workspaces — Google
positions it for dispatching long-running maintenance work or bug fixes in the
background, including tasks that span reproducing an issue, generating a test case and
implementing a fix.

Agents work across the editor, terminal and browser within one task. Google's worked
example has an agent write code for a feature, use the terminal to launch the
application, then use the browser to test and verify the new component, without
synchronous human intervention.

Verification is mediated by **Artifacts** — deliverables the agent generates, such as
task lists, implementation plans, screenshots and browser recordings. Google's stated
rationale is that these let a developer check the agent's logic at a glance where
scrolling raw tool calls would be tedious. Feedback can be left directly on an Artifact,
comparably to commenting on a document, and the agent incorporates that input without
halting its execution flow. Google also states the platform treats learning as a core
primitive, allowing agents to save useful context and code snippets to a knowledge base
to improve future tasks.

## Adoption & Ecosystem

At its announcement the platform was released in public preview, at no cost for
individuals, and cross-platform across macOS, Windows and Linux. Google stated it
offered model optionality: generous rate limits on Gemini 3 Pro, with full support for
Anthropic's Claude Sonnet 4.5 and OpenAI's GPT-OSS. This availability and model list
describe the platform as announced in November 2025.
