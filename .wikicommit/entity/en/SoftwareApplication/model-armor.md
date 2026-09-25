---
title: "Model Armor"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-safety, guardrails, prompt-injection, security]
sources:
  - type: url
    url: 'https://developers.googleblog.com/build-zero-trust-ai-agents-that-judge-intent-not-just-syntax/'
    hash: sha256:d0187b744f61bdd8948c7e820262e3fe8ca76ef50a4f6f3fdec012eb9e39c3b8
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Google Cloud in-line AI firewall that screens prompts and responses for prompt injection, jailbreaks, malicious URLs and sensitive data leakage. On Gemini Enterprise Agent Platform it is applied by Agent Gateway in the request path of an agent."
  applicationCategory: "Managed AI security service"
  featureList: "Ingress screening of prompts for prompt injection, jailbreaks and malicious URLs; blocking of matching requests before the model runs; egress Sensitive Data Protection that redacts sensitive data in responses; regional configuration templates"
  author: "[[Organization/google]]"
---

Model Armor is a Google Cloud service that Google describes as an in-line AI firewall: it screens prompts and responses for prompt injection, jailbreaks, malicious URLs and sensitive data leakage. In [[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] it is one of three managed runtime controls on [[SoftwareApplication/gemini-enterprise-agent-platform]], applied through Agent Gateway, the runtime enforcement point that intercepts interactions between the user, the agent, its model and its tools.

The post presents it as the replacement for a hand-maintained list of jailbreak phrases: maintaining regex dictionaries for every obfuscated jailbreak, it argues, fails quickly in production.

## Capabilities

At ingress, Model Armor screens the payload at the perimeter before the agent's reasoning loop runs. On the platform, Agent Gateway applies a Model Armor template directly in the request path, so the developer does not write the screening call; the post shows the underlying API call, which sends the user prompt against a named template and receives a sanitization result. When a filter matches, the request is dropped at the edge with a 403 — the agent's model is never invoked, so no tokens are consumed and the context window stays clean. The post notes that Model Armor templates are regional.

At egress, it runs Sensitive Data Protection on outgoing responses, redacting values such as credit card numbers, Stripe secrets and employee IDs before they leave the gateway.

## Adoption & Ecosystem

In the post's layered design, Model Armor filters the payload, while [[SoftwareApplication/semantic-governance-policies]] reason about the intent of each proposed tool call and Agent Anomaly Detection watches behaviour over a session. The post's own example shows the limit of payload screening: a polite, syntactically clean social-engineering request carries no jailbreak signal, so Model Armor allows it and the decision falls to the policy engine.
