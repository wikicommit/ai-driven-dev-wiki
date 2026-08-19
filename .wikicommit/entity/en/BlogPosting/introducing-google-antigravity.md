---
title: "Introducing Google Antigravity, a New Era in AI-Assisted Software Development"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, ai-assisted-programming]
sources:
  - type: url
    url: 'https://antigravity.google/blog/introducing-google-antigravity'
    hash: sha256:225ceaf15b2f7d9bdf516bd157b93cadb57a94ac3a9cbcd4464971a5cf516212
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The 18 November 2025 announcement post for [[SoftwareApplication/google-antigravity]], written by the Antigravity Team. It sets out why Google built an agent-first development platform and describes its four stated tenets of collaborative development: trust, autonomy, feedback, and self-improvement."
  author:
    - "The Antigravity Team"
  datePublished: "2025-11-18"
  publisher: "Google"
---

A product announcement post published on 18 November 2025 by the Antigravity Team, introducing [[SoftwareApplication/google-antigravity]] as Google's new agentic development platform. Beyond announcing availability, the post argues a position about where development tooling is heading: that advances in model intelligence for coding repeatedly force a rethink of how development should be done, and that Gemini 3 represents a step-change for agentic coding large enough to require rethinking what the next step-change of an IDE should be.

The post's central claim is that models have started to reach a point of agentic intelligence where they can run for longer periods without intervention across multiple surfaces — "not yet for days at a time," but approaching a world where users interface with agents at higher abstractions than individual prompts and tool calls. Antigravity is presented as Google's answer to what the product surface should look like in that world.

## Key Points

- Antigravity is introduced as an agentic development platform whose core is a familiar AI-powered IDE experience, extended with browser control capabilities, asynchronous interaction patterns, and an agent-first product form factor.
- The post names four tenets it says Antigravity is the first product to bring together: trust, autonomy, feedback, and self-improvement.
- On trust, it criticises two existing extremes — products that show every tool call, and products that show only the final code change with no context — arguing that neither engenders user trust, and that agentic work should instead be presented at a task-level abstraction backed by Artifacts and verification results.
- On autonomy, it introduces the Manager surface as a counterpart to the Editor view, describing it as flipping the paradigm from agents embedded within surfaces to surfaces embedded into the agent.
- On feedback, it argues that a remote-only form factor fails because an agent completing 80% of the work becomes more work than benefit if there is no easy way to resolve the remaining 20%.
- On self-improvement, it describes agent actions as both retrieving from and contributing to a knowledge base, allowing the agent to learn from past work.
- The public preview is announced as free for individuals, compatible with MacOS, Linux, and Windows, and offering access to Google's Gemini 3, Anthropic's Claude Sonnet 4.5 models, and OpenAI's GPT-OSS.

## Context

The post is a vendor's own announcement of its own product and states its positions as Google's vision rather than as findings — it describes what the team believes the next form factor should be, not measured results. A footnote qualifies the preview's rate limits: access is provided to the degree Google has capacity, limits refresh every five hours and correlate with the amount of work an agent does rather than with a prompt count, so the number of prompts available varies with task complexity.
