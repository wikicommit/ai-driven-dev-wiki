---
title: "Utah"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-harness, durable-execution]
sources:
  - type: url
    url: 'https://www.inngest.com/blog/your-agent-needs-a-harness-not-a-framework'
    hash: sha256:7123c66145498ab1e1f577792f9a542f2ac18ddf3ab8acc8c2c0c4af7748b4e4
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Universally Triggered Agent Harness: a conversational Telegram or Slack agent with tools, memory and sub-agent delegation, built by Inngest from Inngest functions, steps and events around a think–act–observe loop, and published as a reference implementation."
  applicationCategory: "Agent harness (reference implementation)"
  featureList: "Agent loop in which every LLM call and tool execution is an Inngest step; provider-agnostic LLM layer (Anthropic, OpenAI, Google) via pi-ai; file, shell and search tools from pi-coding-agent plus remember, web_fetch and delegate_task; sub-agent delegation via step.invoke(); Telegram and Slack webhook integration via Inngest webhook transforms; context pruning, compaction and overflow recovery; session-aware singleton concurrency"
  author: "Inngest"
---

Utah — short for Universally Triggered Agent Harness — is a conversational agent for Telegram or Slack
with tools, memory, sub-agent delegation and full durability, built by Inngest and introduced in
[[BlogPosting/your-agent-needs-a-harness-not-a-framework]]. It is written in minimal TypeScript with no
agent framework: Inngest functions, steps and events provide the harness around a standard
think → act → observe loop. The company built it to show that durable, event-driven infrastructure can
serve as an agent's [[DefinedTerm/agent-harness]], and the post likens it to a durable, cloud-ready
[[SoftwareApplication/openclaw]]. Its source code is published as a reference implementation at
<https://github.com/inngest/utah>.

"Universally triggered" means the agent does not know or care how it was activated — a chat webhook, a
cron schedule, a sub-agent invocation or an inter-function event — so a new channel can be added without
changing the agent loop.

## Capabilities

Chat webhooks reach Inngest Cloud, where a webhook transform turns the raw HTTP payload into a typed
event. A worker running locally, connected to Inngest Cloud over a persistent WebSocket without needing a
public endpoint, picks up the event, runs the agent, and emits a reply event that a separate function
sends back through the channel's own API.

- **The agent loop as steps.** Each iteration calls the LLM, executes any tools it asks for, and feeds
  the results back; every LLM call and every tool execution is an Inngest step, so a failed call is
  retried on its own while earlier iterations stay persisted. A text response with no tool calls ends
  the turn.
- **Six functions.** The agent is split into a main loop, a reply sender, a typing indicator that fires
  immediately, a global failure handler, a scheduled heartbeat and a sub-agent function, each with its
  own retry policy, concurrency controls and triggers.
- **Tools.** File reading, writing and editing, shell execution and search come from the
  `pi-coding-agent` library; Utah adds `remember` (notes to a daily log), `web_fetch` and
  `delegate_task`.
- **Sub-agents.** `delegate_task` starts a separate sub-agent run with its own session key, context
  window and durability, using the same tools minus `delegate_task` so it cannot spawn further
  sub-agents, and returns a summary to the parent.
- **One run per conversation.** Singleton concurrency keyed on the session cancels the running loop when
  a new message arrives and restarts it with the latest context.
- **Context management.** Old tool results are soft-trimmed or cleared when context grows large while the
  last three iterations stay intact; the session history is summarized between runs once it passes a
  token threshold; the agent is warned as it nears its iteration limit; and a context-too-large error
  triggers forced [[DefinedTerm/compaction]] and a retry.
- **Model providers.** LLM calls go through `pi-ai`, a provider-agnostic abstraction, so switching
  between Anthropic, OpenAI and Google is a configuration change.

## Adoption & Ecosystem

Utah draws on OpenClaw and the pi coding-agent libraries, which the post names as its inspiration, but
where those handle events and orchestration in memory, Utah hands orchestration to Inngest; the post
credits that separation with traces and step-level inspection, retries, an audit trail of events,
built-in scheduling, and groundwork for distributed, multi-player orchestration. As published it is a
personal, single-player harness that runs on a local machine or a server. Its authors describe steering
mid-run messages as unsolved and list making it multi-player, streaming progress updates,
human-in-the-loop approval flows and letting it build new agents and workflows itself as things they are
exploring.
