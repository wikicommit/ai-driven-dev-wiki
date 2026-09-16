---
title: "Harness-as-a-Service"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agent-harness-engineering/'
    hash: sha256:7fc8b9bc3a19589c08e3c6ab46607839f3c435799f128886bea9bca6cd634760
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A framing (attributed to Viv Trivedy) for building agents on top of a harness runtime — the loop, tools, context management, hooks, and sandbox primitives — rather than directly on a raw LLM completion API."
---

Harness-as-a-Service (HaaS) is a framing, attributed to Viv Trivedy, for a shift in how agents are built: from building on LLM APIs, which return a completion, to building on harness APIs, which return a runtime. Under this framing, a harness framework supplies the agent loop, tool-calling, context management, hooks, and sandbox primitives out of the box, and the builder customizes them along four pillars — system prompt, tools, context, and subagents — rather than assembling a loop, tool-calling, conversation state, and an approval flow from scratch.

## Usage

The source names the Claude Agent SDK, the Codex SDK, and the OpenAI Agents SDK as examples pointing in this direction. It frames this shift as what makes iterating on an agent's design tractable: a builder is tuning an already-well-factored configuration surface rather than rebuilding an agent from the ground up each time something goes wrong.

## When It Applies

It applies to building a new agent-based product or workflow where a harness framework already covers the loop, tool execution, and context management needs, leaving the differentiating work to domain-specific prompt and tool design. The source quotes Viv Trivedy's argument for starting with an imperfect first version regardless — "good agent building is an exercise in iteration. You can't do iterations if you don't have a v0.1" — as a reason not to delay adopting the pattern until the harness is fully worked out.

## Related Terms

[[DefinedTerm/harness-engineering]]
