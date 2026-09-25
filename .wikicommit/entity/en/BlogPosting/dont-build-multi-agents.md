---
title: "Don’t Build Multi-Agents"
type: "schema:BlogPosting"
lang: en
tags: [agents, multi-agent-systems, context-engineering]
sources:
  - type: url
    url: https://cognition.ai/blog/dont-build-multi-agents
    hash: sha256:c456bd571f488ee46bc4c213e9d4302677f283c444dd4b85a1ad7fa1bd41d480
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A June 2025 post on Cognition's blog arguing that multi-agent architectures, in which subagents work on parts of a task in parallel, produce fragile systems. It sets out two principles of context engineering — share full context and agent traces, and recognise that actions carry implicit decisions — and recommends single-threaded agents instead."
  author: ["Walden Yan"]
  datePublished: "2025-06-12"
  publisher: "[[Organization/cognition]]"
---

*Don’t Build Multi-Agents* is a post on the blog of [[Organization/cognition]], the company behind
[[SoftwareApplication/devin]], that argues against a then-popular way of building AI agents: splitting a
task among several subagents that work in parallel and combining their results. Its starting point is
that building agents still lacks the kind of shared philosophy React gave web development, and that some
libraries — it names OpenAI's Swarm and Microsoft's AutoGen — actively push multi-agent architectures,
which the author considers the wrong way to build agents.

The post places reliability for long-running agents at the centre and names
[[DefinedTerm/context-engineering]] as its core — which it describes as the next level of prompt
engineering, doing the work of supplying a model with the right context automatically in a dynamic
system, and effectively the most important job of engineers building AI agents. From a worked example it
derives two principles, argues that architectures violating them should be ruled out by default, and
recommends a single-threaded linear agent, optionally extended with a model that compresses the history
of actions and conversation for very long tasks.

## Key Points

- The post's example is a "Flappy Bird clone" split into a background subtask and a bird subtask: one
  subagent misreads its subtask and builds a background in another game's style, the other builds a bird
  that does not match, and the final agent is left combining two miscommunications.
- Copying the original task to each subagent is not enough, because in a production system the
  conversation is multi-turn and earlier tool calls and details may all bear on how the task should be
  interpreted.
- Principle 1: share context, and share full agent traces, not just individual messages.
- Even with shared context, parallel subagents that cannot see each other's work make choices based on
  conflicting assumptions, giving inconsistent results — which the post states as Principle 2: actions
  carry implicit decisions, and conflicting decisions carry bad results.
- The simplest architecture that follows both principles is a single-threaded linear agent, whose context
  is continuous; its limit is context-window overflow on very large tasks.
- For truly long tasks the post presents one option: a separate LLM whose purpose is to compress the
  history of actions and conversation into key details, events and decisions — which it calls hard to get
  right, noting that Cognition has fine-tuned a smaller model for this.
- It describes [[SoftwareApplication/claude-code]], as of June 2025, as spawning subtasks but never
  running them in parallel with the main agent and usually giving them only a question to answer rather
  than code to write, keeping the subagent's investigative work out of the main agent's history.
- It cites the [[DefinedTerm/edit-apply-model]] pattern of 2024 as another design that suffered from
  miscommunication between models, and notes that edit decisions and their application are now more often
  made by a single model in one action.
- It judges that in 2025 agents cannot yet resolve disagreements through long-context dialogue with each
  other much more reliably than a single agent, so collaborating agents produce fragile systems with
  decisions too dispersed and context not shared thoroughly enough; the author expects this to improve as
  single-threaded agents get better at communicating with humans.

## Context

The post is written from the perspective of a company building its own agent product, and presents its
principles as ones Cognition's team keeps relearning and builds its internal tools and frameworks around.
It reports no measurements, and the author expects the field's standards to change, calling for some
flexibility and humility.
