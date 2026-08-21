---
title: "Scaling Managed Agents: Decoupling the brain from the hands"
type: "schema:TechArticle"
lang: en
tags: [agent-harness, architecture, long-horizon-agents, security]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/managed-agents'
    hash: sha256:0e4e8bf6d9cb724da07f95297d00f7077a224890c85346851d0d455eba93d529
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Anthropic's account of the architecture behind Managed Agents, which virtualises an agent into three independently replaceable interfaces — session, harness and sandbox — so that the abstractions outlast any particular harness implementation."
  author: ["Lance Martin", "Gabe Cemaj", "Michael Cohen"]
  datePublished: "2026-04-08"
  publisher: "[[Organization/anthropic]]"
  proficiencyLevel: "Advanced"
---

This post explains the architecture behind [[SoftwareApplication/claude-managed-agents]], and the reasoning that produced it. Its premise is that a harness encodes assumptions about what the model cannot do on its own, and that those assumptions go stale as models improve — so the durable design problem is how to build for "programs as yet unthought of."

Its worked example of staleness is concrete: in prior work, Claude Sonnet 4.5 would wrap up tasks prematurely as it sensed its context limit approaching, a behaviour the post calls **context anxiety**, and the fix was to add context resets to the harness. Running the same harness on Claude Opus 4.5 showed the behaviour was gone, and the resets had become dead weight.

The analogy it builds from is operating systems, which lasted decades by virtualising hardware into abstractions — process, file — general enough for programs that did not yet exist, so that `read()` is agnostic as to whether it is reaching a 1970s disk pack or a modern SSD. Managed Agents virtualises an agent the same way, into a **session** (the append-only log of everything that happened), a **harness** (the loop that calls Claude and routes its tool calls), and a **sandbox** (an execution environment for running code and editing files) — each swappable without disturbing the others.

## Key Practices

**Do not adopt a pet.** The first design put session, harness and sandbox in one container. That made file edits direct syscalls and removed service boundaries, but produced a named, hand-tended server that could not be lost: a failed container lost the session, and an unresponsive one had to be nursed back to health. Debugging was worse than the failures — the only window in was a WebSocket event stream that could not distinguish a harness bug from a dropped packet from an offline container, and getting a shell inside meant entering a container that often also held user data.

**Make the container cattle.** With the harness outside the container, it calls the sandbox the way it calls any other tool: `execute(name, input) → string`. A dead container surfaces as a tool-call error passed back to Claude; if Claude retries, a new one is reinitialised through `provision({resources})`.

**Make the harness cattle too.** Because the session log lives outside the harness, nothing in the harness needs to survive a crash. A replacement is started with `wake(sessionId)`, retrieves the event log through `getSession(id)`, and resumes from the last event; during the loop the harness keeps the record durable with `emitEvent(id, event)`.

**Put credentials out of the sandbox's reach.** In the coupled design, untrusted code Claude generated ran in the same container as credentials, so an [[DefinedTerm/indirect-prompt-injection]] only had to convince Claude to read its own environment — after which an attacker could spawn fresh unrestricted sessions and delegate work to them. The post rejects narrow scoping as the primary answer, on the grounds that it encodes an assumption about what Claude cannot do with a limited token while Claude keeps getting smarter. The structural fix is that tokens are never reachable from the sandbox: for Git, a repository access token clones the repo during sandbox initialisation and is wired into the local remote, so `push` and `pull` work without the agent ever handling it; for custom tools, OAuth tokens sit in a secure vault and Claude calls MCP tools through a dedicated proxy that exchanges a session-associated token for the real credential. The harness is never made aware of any credentials.

**Treat the session as a context object, not a context window.** Compaction and trimming both make irreversible decisions about what to keep, and it is difficult to know which tokens later turns will need. Here the session log is durable storage the agent can interrogate: `getEvents()` selects positional slices of the event stream, so the harness can resume where it stopped reading, rewind a few events before a moment to see the lead-up, or reread context before a specific action. Fetched events may then be transformed in the harness — for prompt-cache hit rate, or any context engineering a future model needs. The stated reason for splitting these concerns is that the specific context engineering required by future models is unpredictable, so the session guarantees only durability and interrogability.

## Scope & Caveats

The reported performance result comes from provisioning containers lazily, through a brain-initiated tool call, so a session that does not need a container immediately does not wait for one and inference can begin as soon as pending events are pulled. On that architecture p50 time-to-first-token dropped roughly 60% and p95 dropped over 90%. These are Anthropic's own figures for its own service.

The "many hands" direction is presented as newly viable rather than long-planned: the single container was chosen originally because earlier models were not capable of reasoning about many execution environments and deciding where to send work. As intelligence scaled, the single container became the limitation, since its failure lost state for every hand the brain was reaching into. Because a hand is only `execute(name, input) → string`, the harness does not know whether a sandbox is a container, a phone, or a Pokémon emulator, and hands can be passed between brains.

The post positions the result as a [[DefinedTerm/meta-harness]] — deliberately unopinionated about which specific harness Claude will need, while opinionated about the interfaces around it.
