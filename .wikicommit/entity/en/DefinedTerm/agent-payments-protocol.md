---
title: "Agent Payments Protocol (AP2)"
type: "schema:DefinedTerm"
lang: en
aliases: ["AP2"]
tags: [agents, agent-protocols, agentic-commerce, guardrails]
sources:
  - type: url
    url: 'https://developers.googleblog.com/developers-guide-to-ai-agent-protocols/'
    hash: sha256:7b380e1b02a7431f86ce85fd5ad5a49d2707ee157205f5584f28284782319fef
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A protocol for authorizing purchases made by AI agents, using typed mandates that provide non-repudiable proof of intent and enforce configurable guardrails such as approved merchants and spending limits, and producing an audit trail from intent through signed mandate to receipt."
---

The Agent Payments Protocol (AP2) is a protocol for authorizing payments that AI agents make on a
user's behalf. [[BlogPosting/developers-guide-to-ai-agent-protocols]] describes it as adding typed
mandates that provide non-repudiable proof of intent and enforce configurable guardrails on every
transaction, so that an agent's purchases carry a record of what limits were set, which merchants were
approved, when the authorization expires, and who approved each payment.

## Usage

The guide introduces AP2 at the point where an agent has already gained the ability to place orders and
the open question is who authorized the spending. Its flow has three typed objects. An
`IntentMandate`, configured by the owner, specifies the allowed merchants, conditions such as
refundability, whether cart confirmation is required, a spending limit for auto-approval and an expiry.
The agent then generates a `PaymentMandate` bound to a specific cart and amount; if the order exceeds
the limit, the mandate remains unsigned until a manager explicitly approves it. A `PaymentReceipt`
closes the audit trail. The guide summarizes the chain as recording what was intended, authorized and
paid.

AP2 is designed to work with the [[DefinedTerm/universal-commerce-protocol]]: in the guide's words, UCP
handles what is ordered and from whom, while AP2 handles who approved the purchase and provides the
audit trail, plugging into UCP as an extension that adds cryptographic proof of authorization to the
checkout flow. The guide's example simulates the manager's signature and notes that real AP2 uses
JWT or biometric signing on a secure device.

At the time of that post AP2 was at v0.1, and its types were provided as a separate package rather than
built into the core of [[SoftwareApplication/agent-development-kit]].

## Related Terms

- [[DefinedTerm/universal-commerce-protocol]] — the commerce protocol AP2 extends
- [[DefinedTerm/guardrails]] — AP2's mandates are a protocol-level form of spending guardrail
- [[DefinedTerm/human-in-the-loop]] — orders over the configured limit wait for explicit human approval
