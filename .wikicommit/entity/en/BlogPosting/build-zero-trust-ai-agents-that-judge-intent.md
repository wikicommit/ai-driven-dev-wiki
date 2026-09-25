---
title: "Build zero-trust AI agents that judge intent, not just syntax"
type: "schema:BlogPosting"
lang: en
tags: [agent-safety, guardrails, governance, prompt-injection, security]
sources:
  - type: url
    url: 'https://developers.googleblog.com/build-zero-trust-ai-agents-that-judge-intent-not-just-syntax/'
    hash: sha256:d0187b744f61bdd8948c7e820262e3fe8ca76ef50a4f6f3fdec012eb9e39c3b8
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Part 2 of a Google for Developers series on zero-trust agents. It moves the security checks of a customer-support refund agent from build-time code into managed runtime governance on Gemini Enterprise Agent Platform, where Model Armor, Semantic Governance Policies and Agent Anomaly Detection reason about intent and behaviour rather than syntax."
  author: ["Eric Dong", "Shubham Saboo"]
  datePublished: "2026-09-15"
  publisher: "[[Organization/google]]"
---

This post is the second part of a series on zero-trust agents. Part 1 had established three deterministic controls for autonomous agents — signed database writes with Cloud KMS, user-space kernel isolation with gVisor, and an input/output gateway backed by CI unit tests. Part 2 starts from the limit those controls share: they only catch cases that can be explicitly specified ahead of time. A SQL parser cannot tell a socially engineered refund from a legitimate one if the syntax is valid, a regex cannot tell a physical USB cable from an opened software license, and a single-turn test suite cannot see an agent being drained across several turns.

The post keeps the same Customer Support & Returns Agent built with [[SoftwareApplication/agent-development-kit]] and deploys it to [[SoftwareApplication/gemini-enterprise-agent-platform]], replacing self-hosted container infrastructure and hand-maintained regex lists with three managed controls applied through Agent Gateway, the runtime enforcement point between the user, the agent, its model and its tools: [[SoftwareApplication/model-armor]], [[SoftwareApplication/semantic-governance-policies]] and Agent Anomaly Detection. It walks through the attacks the build-time controls let through against a single example order, and closes with a closed-loop remediation that answers a detected anomaly with a new policy.

The post also argues that moving the checks to the platform changes who owns them: governance is defined and managed by a platform or security administrator, separate from the agent developer, because the platform enforces it outside the agent code.

## Key Points

- The post's premise is that a zero-trust runtime assumes each individual request can look valid and still be part of an attack, so rules cannot all be hard-coded in advance.
- Model Armor is described as an in-line AI firewall that screens prompts at the ingress perimeter, before the agent's reasoning loop runs, for prompt injection, jailbreaks and malicious URLs; a matching request is dropped with a 403, so the model is never invoked and no tokens are consumed.
- At egress, Model Armor is described as running Sensitive Data Protection on outgoing responses, redacting data such as credit card numbers and secrets before they leave the gateway.
- A polite, syntactically clean request to refund a $120.00 annual software license passes every deterministic gate; the post's argument is that keyword matching fails because the request names a "Google Workplace user license" rather than saying "software".
- Semantic Governance Policies are described as an LLM-based natural-language policy engine that evaluates each proposed tool call and its parameters against the user prompt, the conversation history and plain-text business rules before the call runs, and suppresses it on a DENY verdict.
- The post states that Semantic Governance applies regardless of whether the agent reaches the tool directly in code or remotely through an API endpoint or an MCP server.
- A multi-turn exploit — eight $20.00 refunds on a $149.00 order, each individually allowed — is presented as something single-turn guardrails cannot see, because they evaluate each request in isolation.
- Agent Anomaly Detection is described as monitoring session telemetry across the fleet with statistical models and LLM analysis; the companion demo's local stand-in keys on tool-call velocity, repeated writes against one entity and cumulative parameter values. The post says the detector names, confidence values and finding shape it shows are illustrative.
- Remediation is closed without modifying or redeploying agent code: an administrator, or an automated process through APIs, authors a new natural-language constraint, which the policy engine then applies to the next tool call.
- The post presents these runtime controls as mapping one to one onto the build-time controls of Part 1, forming defense in depth rather than replacing them.

## Context

The post is written by Google staff about Google Cloud products, and its claims about Model Armor, Semantic Governance Policies and Agent Anomaly Detection are the vendor's own descriptions demonstrated on a single example transaction, not measured results. It notes that in production an agent would typically reach its tools through the Model Context Protocol or backend APIs, while the companion demo implements them as local Python functions for simplicity, and that the demo runs locally with no external dependencies. It describes the three runtime controls as each covering what the others cannot: Model Armor filters the payload, the policy engine reasons about intent, and anomaly detection watches behaviour over time.
