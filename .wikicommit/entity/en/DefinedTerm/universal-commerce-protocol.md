---
title: "Universal Commerce Protocol (UCP)"
type: "schema:DefinedTerm"
lang: en
aliases: ["UCP"]
tags: [agents, agent-protocols, agentic-commerce]
sources:
  - type: url
    url: 'https://developers.googleblog.com/developers-guide-to-ai-agent-protocols/'
    hash: sha256:7b380e1b02a7431f86ce85fd5ad5a49d2707ee157205f5584f28284782319fef
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A protocol that standardizes the shopping lifecycle for AI agents into modular capabilities with strongly typed request and response schemas, kept consistent across REST, MCP, A2A and embedded browser protocols, so that an agent can order from different merchants through one pattern."
---

The Universal Commerce Protocol (UCP) is a protocol for letting AI agents buy things through one
pattern rather than one integration per merchant. As described in
[[BlogPosting/developers-guide-to-ai-agent-protocols]], it standardizes the shopping lifecycle into
modular capabilities, expressed as strongly typed request and response schemas that remain consistent
whatever the underlying transport — REST, [[DefinedTerm/model-context-protocol]],
[[DefinedTerm/agent2agent-protocol]], or Embedded Protocols (EP) for browser-based flows.

## Usage

The problem UCP addresses, in that guide's framing, is that every supplier has a different checkout
API, so an agent sourcing from five wholesale distributors would otherwise need five different checkout
integrations. With UCP, the agent discovers a merchant's capabilities from a profile published at a
well-known URL (`/.well-known/ucp`) — the same discovery pattern A2A uses for its Agent Cards — then
builds a typed checkout request with line items and payment details, creates a checkout session, and
completes it. The guide's example sends identifying headers with each request, including one pointing
to the calling agent's capability profile and a fresh idempotency key per operation.

Because UCP also supports a standard REST API, the guide notes that it works with whatever HTTP client
a project already uses, with no proprietary SDK required. It also points to a sample shopping assistant
that combines UCP with A2A for end-to-end shopping workflows.

UCP covers what is ordered and from whom. Authorization for the purchase — who approved it, within what
limits — is the job of the [[DefinedTerm/agent-payments-protocol]], which the guide describes as
plugging into UCP as an extension.

## Related Terms

- [[DefinedTerm/agent-payments-protocol]] — adds payment authorization and an audit trail to UCP's
  checkout flow
- [[DefinedTerm/agent2agent-protocol]] — whose well-known-URL discovery pattern UCP reuses
- [[DefinedTerm/model-context-protocol]] — one of the transports UCP can run over
