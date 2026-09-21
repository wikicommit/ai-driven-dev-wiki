---
title: "LiteLLM"
type: "schema:SoftwareApplication"
lang: en
tags: [llm-gateway, model-routing, enterprise-adoption]
sources:
  - type: url
    url: 'https://engineering.zalando.com/posts/2026/08/agentic-engineering-at-zalando-a-snapshot.html'
    hash: sha256:33171882bb4809ae93923b09f4e1fe6315bf6de5690393243df5a995118678bc
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An extensible API proxy for large language models, used to place a single internally operated endpoint in front of several model providers. This wiki's account of it comes from one organization's deployment rather than from its own documentation."
  applicationCategory: "LLM gateway / API proxy"
  featureList: "Multi-provider model access; pre-call and post-call hooks; prompt caching checkpoint auto-injection; request-count-based restarts"
---

LiteLLM is an API proxy for large language models that presents one endpoint in front of several
model providers. What this wiki records about it comes from a single deployment account rather
than from the project's own documentation: [[Organization/zalando]]'s ML platform team deployed a
LiteLLM-based proxy in January 2024 to give its engineers API-based access to models alongside the
IDE autocomplete they already had, and described the result in
[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]].

In that deployment the proxy fronts models from OpenAI, AWS Bedrock and Google Vertex, and the
stated reason for putting it there was twofold: engineers could experiment with different tools
and models easily, and the platform team gained a single point at which to measure adoption — by
monthly and weekly active users, by model, and by User-Agent.

## Capabilities

The capability the source singles out is extensibility through hooks. Zalando reports using
post-call hooks for anonymized cost tracking and pre-call hooks to enforce client version upgrades,
restricting access to the proxy based on the User-Agent header. It also reports enabling
auto-injection of prompt caching checkpoints, which it says reduced costs for custom agents whose
authors were still learning about prompt caching.

Two operational details are reported from the same deployment. To mitigate stability and memory
leak issues, that team enforces restarts after 20,000 requests using a
`--max_requests_before_restart` setting, and states that this lets it serve 2,000 monthly active
users from six pods of two CPU cores and 4 GB of memory each. The post also says the team looks
forward to a Rust rewrite expected to improve performance and stability; that is an expectation
recorded in August 2026, not a shipped state.

## Adoption & Ecosystem

The pattern this account illustrates is a self-hosted gateway used as the enforcement point for an
organization's model access policy. Because every request passes through it, the proxy is where
adoption is measured, where costs are attributed, where client versions are forced forward, and
where retired models are taken out of reach — the post notes that for self-managed client
installations, blocking access is the only effective measure, since there is always a long tail of
users who do not update their local configuration.

The same account names two recurring problems with the LLM-enabled tools that sit in front of such
a proxy, neither specific to LiteLLM: tools too often send a generic User-Agent header, making
clients hard to identify, and they lack support for custom auth commands, defaulting to static
credentials whose expiry then requires manual refreshes and application restarts.
