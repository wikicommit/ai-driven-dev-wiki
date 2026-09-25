---
title: "Your Agent Needs a Harness, Not a Framework"
type: "schema:BlogPosting"
lang: en
tags: [agents, agent-harness, durable-execution, context-management]
sources:
  - type: url
    url: 'https://www.inngest.com/blog/your-agent-needs-a-harness-not-a-framework'
    hash: sha256:7123c66145498ab1e1f577792f9a542f2ac18ddf3ab8acc8c2c0c4af7748b4e4
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A March 2026 post on the Inngest blog arguing that an agent runtime needs a harness — the layer that connects, protects and orchestrates the LLM, tools and memory — and that durable, event-driven infrastructure already provides one. It presents Utah, a reference implementation built on Inngest functions, steps and events."
  author: ["Dan Farrelly"]
  datePublished: "2026-03-03"
  publisher: "Inngest"
---

*Your Agent Needs a Harness, Not a Framework* is a post on the Inngest blog. It starts from the
engineering meaning of a harness — a wiring harness, a test harness, a safety harness: the layer that
connects, protects and orchestrates components without doing the work itself — and argues that agent
runtimes need the same thing. In its framing the LLM is the engine, tools are the peripherals and memory
is storage, and the open question is what connects them, catches a failure when the LLM times out
mid-loop, prevents two messages from colliding, and routes an event to the right handler and reply
channel. The post observes that every agent framework is building such a harness from scratch, with its
own retry logic, state persistence, job queues and event routing.

Its answer is that durable, event-driven infrastructure already solves this: if every LLM call or tool
call is a step — an independently retryable unit of work — then work already done is persisted when a
process dies, events route triggers between functions, concurrency controls prevent collisions, and
step-level traces make every iteration of the agent loop observable. To demonstrate this the company
built [[SoftwareApplication/utah]] (Universally Triggered Agent Harness), which the post describes as a
durable, cloud-ready take on [[SoftwareApplication/openclaw]] and publishes as a reference implementation.

## Key Points

- A harness, in the post's sense, connects, protects and orchestrates an agent's components without doing
  the work itself; it frames the problems a harness solves — retries, state, concurrency, observability,
  scheduling — as infrastructure problems rather than AI problems.
- Making every LLM call and every tool execution a step means a failed call is retried on its own while
  the results of earlier iterations are already persisted and are not re-executed.
- Decoupling the trigger from the work lets the same agent loop be activated by chat webhooks, cron
  schedules, sub-agent invocations or inter-function events without changing; this is what the
  "universally triggered" in Utah's name refers to.
- Splitting the agent into small functions connected by events — a main loop, a reply sender, an
  immediate typing indicator, a global failure handler, a scheduled heartbeat and a sub-agent function —
  gives each its own retry policy, concurrency controls and trigger conditions.
- A sub-agent can be run as a separate function invocation with its own context window and the same tools
  minus the delegation tool, returning a summary to the parent; the post presents this as orchestration
  without any agent-to-agent protocol.
- Concurrency keyed on the conversation, set to cancel the running loop when a new message arrives,
  keeps one agent run per chat and restarts it with the latest context.
- The authors report that context management, not calling the LLM, was the hardest problem: large tool
  results made the loop call tools endlessly without replying, which they addressed with two-tier pruning
  of old tool results, session-level [[DefinedTerm/compaction]], budget warnings near the iteration limit,
  and forced compaction on context-overflow errors.
- Steering — what should happen when a user sends a new message mid-run — is presented as unsolved:
  cancel-and-restart works but loses in-flight work.

## Context

The post is written by the vendor of the infrastructure it recommends and closes by inviting readers to
try Inngest, so its argument that existing primitives already form a harness doubles as a case for that
product. Its evidence is the team's own experience building Utah; it reports no measurements. It
describes Utah as a personal, single-player harness and lists making it multi-player, streaming or
mid-loop progress updates, human-in-the-loop approvals and letting the agent extend itself as directions
still being explored. Its use of "harness" for the connecting runtime layer is one of several framings of
the term on this wiki; see [[DefinedTerm/agent-harness]].
