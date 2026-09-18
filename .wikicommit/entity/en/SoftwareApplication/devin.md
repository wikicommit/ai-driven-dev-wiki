---
title: "Devin"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Cognition's autonomous coding agent, cited as an emerging example of goal-agentic (Level 3, SE3.0) AI software engineering that can take a well-defined technical goal and execute a multi-step plan across code, documentation, and other project artifacts."
  applicationCategory: "Autonomous coding agent"
  author: "Cognition"
---

Devin is Cognition's autonomous coding agent, discussed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] alongside Google's [[SoftwareApplication/google-jules]], OpenAI's Codex, and Anthropic's [[SoftwareApplication/claude-code]] as an example of an agent aiming for Goal-Agentic (Level 3, SE3.0) capability in the paper's [[DefinedTerm/se-autonomy-levels]] hierarchy: taking a well-defined technical goal (e.g. "add a caching layer") and executing a multi-step plan, self-devised or human-guided, across code, documentation, and other essential project artifacts.

## Capabilities

The paper cites DeepWiki, used by Devin, as an early example of a persistent-memory capability: it lets the agent build and refer to its own documentation and decision logs across multiple tasks, creating continuity and helping prevent it from repeating past mistakes — an example the paper uses to motivate its proposed [[DefinedTerm/ai-teammate-lifecycle-engineering]] activity.

## Adoption & Ecosystem

Devin is named, alongside OpenAI's Codex, GitHub Copilot, Cursor, and Claude Code, as one of five agent tools whose pull requests were aggregated in the [[Dataset/aidev]] dataset of 932,791 agent-authored GitHub pull requests.
