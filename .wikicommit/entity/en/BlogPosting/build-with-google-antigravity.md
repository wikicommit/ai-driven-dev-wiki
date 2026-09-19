---
title: "Build with Google Antigravity, our new agentic development platform"
type: "schema:BlogPosting"
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
  description: "Google's announcement post introducing Antigravity, an agentic development platform built around an agent-first Manager surface and agent-generated Artifacts for verification."
  author: ["Google Antigravity Team"]
  datePublished: "2025-11-20"
  publisher: "[[Organization/google]]"
---

Google's announcement post introducing [[SoftwareApplication/google-antigravity]], which
it describes as not just an editor but an agentic development platform. The post's framing
argument is that the previous generation of tools helped developers write code faster,
while the next generation needs to help them orchestrate it — so the platform is designed
for working at what the post calls a higher, task-oriented level.

The post's central design claim is that agents should not be chatbots in a sidebar but
should have a dedicated space of their own — in its words, that agents "shouldn't just be
chatbots in a sidebar" — and it introduces two surfaces to that end: a
familiar AI-powered editor for synchronous work, and a Manager surface for spawning
and observing multiple agents working asynchronously across workspaces. Its second claim
concerns verification — that delegating work requires trust, and that scrolling raw tool
calls does not build it — which the post answers with Artifacts, tangible deliverables an
agent produces for review.

## Key Points

- The post frames agentic development as a shift from writing code faster to
  orchestrating it, and states as a design belief that agents should not just be chatbots
  in a sidebar but should have their own dedicated space to work.
- Two interaction surfaces are offered: an Editor View with tab completions and inline
  commands for hands-on synchronous work, and a Manager surface where multiple agents are
  spawned, orchestrated and observed working asynchronously across different workspaces.
- Agents are described as operating across the editor, terminal and browser within a
  single task — the post's example has an agent write a feature, launch the application
  from the terminal, then drive the browser to verify the component works, without
  synchronous human intervention.
- Verification is done through Artifacts rather than logs: task lists, implementation
  plans, screenshots and browser recordings, which the post argues let a developer check
  the agent's logic at a glance.
- Feedback is left directly on an Artifact, in the manner of commenting on a document,
  and the post states the agent incorporates that input without stopping its execution
  flow.
- The post states the platform treats learning as a core primitive, letting agents save
  useful context and code snippets to a knowledge base to improve future tasks.
- At announcement the platform was in public preview at no cost for individuals, on
  macOS, Windows and Linux, with Gemini 3 Pro plus support for Anthropic's Claude Sonnet
  4.5 and OpenAI's GPT-OSS. These are the terms and model list stated at launch.

## Context

This is a first-party product announcement published on Google's own developer blog, so
its claims about what the platform does are the vendor's own description rather than
independent evaluation. The post reports no usage data, benchmark or user study.

Its verification-through-Artifacts argument addresses the same difficulty as other work
on keeping a person meaningfully in control of an autonomous agent — see
[[DefinedTerm/human-in-the-loop]] and the [[DefinedTerm/review-bottleneck]] — by changing
what the agent hands the human to read. The asynchronous
Manager surface places it among tools organized around
[[DefinedTerm/long-running-agent]] work and the [[DefinedTerm/outer-loop]].
