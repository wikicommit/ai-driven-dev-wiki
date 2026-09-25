---
title: "Brain/Hands/Session Split"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  - type: url
    url: 'https://www.anthropic.com/engineering/managed-agents'
    hash: sha256:058bb96f68b5ec148e00110cca6d9517e4d5dcba8d1d14b840b8aef1a5da3ed2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An architectural pattern that decouples an AI agent into three independently replaceable components: the Brain (the model and the harness loop that calls it), the Hands (sandboxes and tools that perform actions), and the Session (an append-only log of the session's events)."
---

The Brain/Hands/Session split is a pattern, set out by Anthropic in
[[BlogPosting/scaling-managed-agents-decoupling-the-brain-from-the-hands]], for building a long-running
AI agent by separating it into three components that can each fail or be replaced independently. The
Brain is Claude together with its harness, the loop that calls the model and routes its tool calls. The
Hands are the sandboxes and tools that perform actions. The Session is an append-only log of everything
that happened. Each becomes an interface that makes few assumptions about the others.

## Usage

The pattern is the architecture of [[SoftwareApplication/claude-managed-agents]]. Anthropic explains it by
analogy with operating systems, which virtualized hardware into abstractions such as the process and the
file that outlasted the hardware beneath them: it aims to be "opinionated about the shape of these
interfaces, not about what runs behind them," because harnesses encode assumptions about what Claude
cannot do on its own and those assumptions go stale as models improve. Its example is a harness that added
context resets to counter [[DefinedTerm/context-anxiety]] in one model, only for the behavior to be gone in
a later model, leaving the resets as dead weight.

Anthropic describes having first run all three components in a single container, which made that
container a "pet" in the pets-versus-cattle sense: if it failed the session was lost, debugging meant
opening a shell in a container that often held user data, and the harness assumed every resource sat next
to it. After decoupling, the harness calls the sandbox like any other tool (`execute(name, input) →
string`), so a failed container becomes a tool-call error and a new one can be provisioned; and because
the session log sits outside the harness, a failed harness can be rebooted with `wake(sessionId)`, fetch
the log with `getSession(id)` and resume from the last event. Anthropic reports that provisioning
containers only when needed dropped time-to-first-token by roughly 60% at p50 and over 90% at p95, and
that the same separation lets one brain work with many hands and many stateless brains be started at
once.

The Session also changes how long contexts are handled. Anthropic distinguishes it from Claude's context
window: rather than making irreversible decisions about what to keep, as [[DefinedTerm/compaction]] and
context trimming do, the session durably stores every event and lets the harness select slices of it, while
any transformation before events reach the model is left to the harness.

Addy Osmani's overview of long-running agents describes Google's Gemini Enterprise Agent Platform as
architecturally the same brain/hands/session split, productized at platform scale and bundled with a
development kit rather than assembled by a team from scratch (see
[[SoftwareApplication/gemini-enterprise-agent-platform]]).

## When It Applies

- **Conditions.** Anthropic presents the pattern for hosting long-horizon agents, where a durable event log
  outside the harness is what makes a run recoverable after a container or harness failure, and where an
  agent may need to reach execution environments beyond a single shell.
- **Assumptions.** It assumes the model can reason about several execution environments and decide where
  to send work. Anthropic notes that it started with a single container because earlier models were not
  capable of this.
- **Security.** Separating the sandbox from the harness is how Anthropic keeps credentials unreachable
  from the sandbox where Claude's generated code runs, so that a prompt injection cannot simply read them
  from the environment; Git tokens are wired into the sandbox's remote at initialization and MCP
  credentials are fetched from a vault by a proxy.
- **How established.** It is one vendor's account of the design of its own hosted service, with
  performance figures from that service; Osmani's overview treats the split as the pattern underlying
  several managed agent runtimes.

## Related Terms

[[DefinedTerm/long-running-agent]], [[DefinedTerm/meta-harness]], [[DefinedTerm/agent-harness]],
[[SoftwareApplication/claude-managed-agents]], [[SoftwareApplication/gemini-enterprise-agent-platform]],
[[Organization/anthropic]]
