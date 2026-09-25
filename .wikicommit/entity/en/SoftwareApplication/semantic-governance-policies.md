---
title: "Semantic Governance Policies"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-safety, guardrails, governance, tool-use]
sources:
  - type: url
    url: 'https://developers.googleblog.com/build-zero-trust-ai-agents-that-judge-intent-not-just-syntax/'
    hash: sha256:d0187b744f61bdd8948c7e820262e3fe8ca76ef50a4f6f3fdec012eb9e39c3b8
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An LLM-based natural-language policy engine on Gemini Enterprise Agent Platform that evaluates each tool call an agent proposes against the user's intent, the conversation history and plain-text business rules, and blocks the call before it runs when the verdict is DENY."
  applicationCategory: "Managed agent runtime governance service"
  featureList: "Plain-text policy constraints targeted at specific tools; pre-execution evaluation of proposed tool calls and parameters; DENY verdicts that suppress tool execution; verdicts logged to Cloud Logging; policies that take effect at runtime without redeploying the agent; policy creation through a console experience or APIs"
  author: "[[Organization/google]]"
---

Semantic Governance Policies is a managed control on [[SoftwareApplication/gemini-enterprise-agent-platform]] that places a natural-language policy engine in front of an agent's tool execution. Google describes it as LLM-based: at the moment the model proposes a tool call, the engine evaluates the tool and the proposed parameters against the user prompt, the conversation history and the configured policies, and returns a verdict. It is enforced through Agent Gateway, outside the agent's own code.

In [[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] it is the answer to requests that pass every syntactic check but violate business intent. The post's example is a polite request to refund a $120.00 annual "Google Workplace user license": the amount is within the order total and the parameters are well typed, but company policy makes digital software licenses over $30 non-refundable without manager approval. Because the request never says "software", the post argues, keyword matching and regex filters miss it, and a SQL parser has no way to know the item is digital software.

## Capabilities

Policies are written as plain-text constraints attached to target tools, so that — in the post's words — a business owner can read and change them; the example policy denies refunds for opened digital goods, software licenses or clearance items over 30 USD and routes them to a human manager, with enforcement set to block. When the engine returns DENY, tool execution is suppressed before it runs — in the example, the signing key is never called and the ledger is untouched — and the agent explains the outcome to the user. Each evaluation is recorded in the Cloud Logging event stream with the tool, a rationale and the verdict. The post notes that the reason for a denial can be configured not to be disclosed.

The post states that Semantic Governance applies regardless of how the agent accesses the tool: directly in code within the agent, or remotely through an API endpoint or an MCP server.

## Adoption & Ecosystem

Because policies are evaluated dynamically at runtime, the post uses them to close the loop on attacks found by Agent Anomaly Detection: an administrator reviews the flagged trace in the Semantic Governance Policies experience and authors a new constraint covering the pattern, or an automated process creates one through APIs, and the new policy applies on the next tool call without modifying, redeploying or restarting the agent. Its example remediation denies any further refund for an order that already had an approved refund in the same session.

The post positions it between [[SoftwareApplication/model-armor]], which filters the payload, and anomaly detection, which watches behaviour over time, and notes that single-turn evaluation of this kind cannot on its own see an exploit split across many individually permitted turns. It also presents moving such checks to the platform as shifting their ownership to a platform or security administrator, separate from the agent developer.
