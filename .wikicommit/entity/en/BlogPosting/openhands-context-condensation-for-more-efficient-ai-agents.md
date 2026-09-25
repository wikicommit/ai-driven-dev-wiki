---
title: "OpenHands Context Condensensation for More Efficient AI Agents"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, context-window, long-horizon-tasks]
sources:
  - type: url
    url: 'https://openhands.dev/blog/openhands-context-condensensation-for-more-efficient-ai-agents'
    hash: sha256:9c162f7d2b9faa097af2bc398adfb790f05ef67863ae29034d68c30367bfb45b
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An April 2025 post on the OpenHands blog introducing the OpenHands context condenser, which summarizes older parts of an agent's conversation once it passes a size threshold, and reporting lower per-turn cost with an equivalent solve rate on a subset of SWE-bench Verified."
  author: ["Calvin Smith"]
  datePublished: "2025-04-09"
  publisher: "OpenHands"
---

This post from the [[SoftwareApplication/openhands]] blog introduces the **OpenHands context
condenser**, which it presents as an advance in the OpenHands agent architecture aimed at managing
growing conversation context. It starts from a problem familiar to anyone who has run an agent on a
long, complex task: as the conversation grows the agent becomes slower, more expensive per turn, and
less effective, because LLMs do worse with lots of irrelevant information in context. Starting a new
chat avoids this but sacrifices continuity and leaves the user to carry context across sessions by
hand.

The condenser keeps the conversation bounded instead. Once the conversation grows beyond a threshold,
older interactions are summarized while recent exchanges are kept intact, giving the agent a concise
"memory" of what happened earlier without retaining every detail. The post headlines three results: up to 2x lower per-turn API cost, consistent response times in long
sessions, and equivalent or better performance on software engineering tasks.

## Key Points

- The summary is meant to encode the user's goals, the progress the agent has made, and what still
  has to be done; for software development tasks it also preserves technical details such as critical
  files and failing tests.
- Condensation fires only when the context reaches a specific size, which the post says keeps the
  benefit of prompt caching by amortizing the cost of rebuilding the cache across multiple turns.
- When events are of similar size, the post argues, baseline context management without condensation
  scales quadratically over time while the condensed approach scales linearly.
- Evaluated against the baseline OpenHands agent on a subset of SWE-bench Verified instances, average
  per-turn cost diverged from the baseline once condensation kicked in and settled at less than half
  of it.
- On that subset the condensing agent solved an average of 54% of instances against the baseline's
  53%, and solved a larger share using less money, fewer tokens and less completion time; the post
  says these trends hold regardless of the breakpoints chosen.
- The one trade-off reported is a higher number of turns, which the post attributes to the agent
  occasionally needing a turn to condense its context.
- All of these results come from OpenHands' own evaluation of its own agent, reported in a post
  announcing the feature.

## Context

The post frames the condenser as a shipped feature: context condensation is available in OpenHands,
including in the managed OpenHands Cloud, where it is described as ready to use. It positions
summarization-based condensation as an alternative to starting a new chat, and treats cost, latency
and effectiveness as the three things long contexts degrade. For other approaches to summarizing an
agent's history as it nears its limits, see [[DefinedTerm/compaction]].
