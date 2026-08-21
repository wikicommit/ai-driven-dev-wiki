---
title: "Claude Managed Agents"
type: "schema:SoftwareApplication"
lang: en
tags: [long-horizon-agents, agent-harness, hosted-service]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/managed-agents'
    hash: sha256:0e4e8bf6d9cb724da07f95297d00f7077a224890c85346851d0d455eba93d529
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A hosted service in the Claude Platform that runs long-horizon agents on a customer's behalf through a small set of interfaces — session, harness and sandbox — designed to outlast any particular harness implementation."
  applicationCategory: "DeveloperApplication"
  author: "[[Organization/anthropic]]"
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

Claude Managed Agents is a hosted service in the Claude Platform that runs long-horizon agents on a customer's behalf. Its design premise, set out in [[TechArticle/scaling-managed-agents]], is that harnesses encode assumptions about what the model cannot do on its own, and that those assumptions go stale as models improve — so the service exposes a small set of interfaces "meant to outlast any particular implementation, including the ones we run today."

## Overview

The service virtualises an agent into three components that can each be swapped without disturbing the others: a **session**, the append-only log of everything that happened; a **harness**, the loop that calls Claude and routes its tool calls to infrastructure; and a **sandbox**, an execution environment where Claude runs code and edits files. Its stated posture is to be opinionated about the shape of those interfaces and not about what runs behind them.

## Features

The interfaces named in that account are `execute(name, input) → string` for invoking a sandbox or any other tool, `provision({resources})` for standing up a fresh sandbox, `wake(sessionId)` for restarting a harness, `getSession(id)` for retrieving the event log, `emitEvent(id, event)` for appending to it during the agent loop, and `getEvents()` for selecting positional slices of the event stream.

Because the session log lives outside both harness and sandbox, a failed sandbox surfaces to Claude as a tool-call error rather than a lost session, and a crashed harness can be replaced by one that wakes on the same session and resumes from the last event. The same durability gives the agent something a context window cannot: the ability to interrogate its own past — resuming where it stopped reading, rewinding to see the lead-up to a moment, or rereading context before a specific action — instead of relying only on irreversible compaction decisions.

Credentials are held outside the sandbox by design. A repository access token is used to clone during sandbox initialisation and wired into the local git remote so `push` and `pull` work without the agent handling it; OAuth tokens for custom tools sit in a secure vault, reached through a dedicated MCP proxy that exchanges a session-associated token for the real credential. The harness is never made aware of any credentials.

## History

The architecture is described as the result of abandoning an earlier design that placed session, harness and sandbox in a single container. That design made the server a "pet" — a failed container lost the session, an unresponsive one had to be nursed back to health, and debugging required entering a container that often held user data. It also assumed everything Claude worked on lived beside it, so customers wanting Claude to reach resources in their own virtual private cloud had to peer networks or run the harness themselves.

Decoupling removed that assumption and, by provisioning containers only when a tool call needs one, produced the reported latency improvement: p50 time-to-first-token down roughly 60% and p95 down over 90%, by Anthropic's own measurement of its own service.
