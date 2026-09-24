---
title: "An important update: Transitioning Gemini CLI to Antigravity CLI"
type: "schema:BlogPosting"
lang: en
tags: [agents, coding-tools, cli]
sources:
  - type: url
    url: 'https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/'
    hash: sha256:74ccc5f44492281655fe5a0f8252a401ded3c57354ca7f1efbbcc7b28d3120f6
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Google's announcement that it is consolidating its terminal coding agent into Google Antigravity: Antigravity CLI becomes generally available and consumer users of Gemini CLI are moved to it, while enterprise-licensed use of Gemini CLI continues."
  author: ["Dmitry Lyalin", "Taylor Mullen"]
  datePublished: "2026-05-19"
  publisher: "[[Organization/google]]"
---

This post announces that Google is folding its terminal agent work into [[SoftwareApplication/google-antigravity]], which it calls its premier agent-first development platform. [[SoftwareApplication/antigravity-cli]] becomes available to everyone on the day of the post, and consumer users of [[SoftwareApplication/gemini-cli]] are to move to it. The post points readers to Google's I/O 2026 updates for more.

The reason given is a change in how developers work. Gemini CLI, the post says, proved the terminal could be a strong interface for agentic tasks, but users now need several agents communicating with each other to split up complex work, which requires terminal tools to share one backend with the rest of the workflow. Google's response is to concentrate on a single product built for what it calls "today's multi-agent reality" rather than maintain two.

## Key Points

- Gemini CLI is described as having grown, since its release the year before, to a community of millions of users, over 100,000 GitHub stars, 6,000 merged pull requests and hundreds of contributors — Google's own figures.
- Antigravity CLI will not have one-to-one feature parity with Gemini CLI at launch, but keeps what the post calls its most critical features: Agent Skills, hooks, subagents, and extensions, which become Antigravity plugins.
- Three improvements are claimed: faster execution because the CLI is built in Go; asynchronous workflows in which multiple agents run in the background without locking the terminal session; and a shared agent harness with the Antigravity 2.0 desktop application, so improvements to core agents reach every surface.
- On June 18, 2026, Gemini CLI and the Gemini Code Assist IDE extensions stop serving requests for Google AI Pro and Ultra subscribers and for free users of Gemini Code Assist for individuals. Gemini Code Assist for GitHub stops accepting new installations on GitHub organizations on the same date, with requests ceasing in the following weeks.
- Enterprise access is unchanged: organizations using Gemini CLI or the IDE extensions under a Gemini Code Assist Standard or Enterprise license, or Gemini Code Assist for GitHub through Google Cloud, keep it, and Gemini CLI remains usable through paid Gemini and Gemini Enterprise Agent Platform API keys.
- Migration is supported through technical documentation, with video walkthroughs promised, and feedback is invited through the Antigravity CLI community forum.

## Context

The post is the vendor's own product announcement, so its account of why the change was made and what users gain from it is Google's framing rather than an outside assessment. It announces a product consolidation, not a deprecation for everyone: Gemini CLI continues for enterprise customers, and what changes is which of Google's two terminal agents consumer users are served by.
