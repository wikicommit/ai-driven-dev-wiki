---
title: "hoop.dev"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-safety, guardrails, human-oversight, security, open-source]
sources:
  - type: url
    url: 'https://hoop.dev/blog/human-in-the-loop-approval-in-ai-coding-agents-explained'
    hash: sha256:d47e37ed6d4309cb36f68927dfc4477de6d95bb29a757d4457974ee26a438f58
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source Layer 7 gateway that sits in the data path between an AI coding agent and the systems it acts on — Git servers, CI pipelines and other endpoints — inspecting each request at the protocol level and applying policy, including holding a change until a human reviewer consents, before anything is forwarded."
  applicationCategory: "Access gateway for AI agents"
  featureList: "Protocol-level proxying of Git servers, CI pipelines and code-related endpoints; policy evaluation before forwarding; human approval routed to a reviewer console; inline masking of detected secrets; session recording and replay; the gateway rather than the agent holds the target credential; OIDC authentication with group-based policy"
---

hoop.dev is an open-source Layer 7 gateway that its makers position between an AI coding agent and
the systems the agent acts on. Rather than letting the agent talk directly to a Git server,
container registry or CI/CD orchestrator, the gateway receives the request, inspects the payload at
the protocol level and applies policy before forwarding anything downstream — and where the policy
calls for it, blocks the forward flow while an authorized reviewer decides.

The vendor's own argument for this placement is that identity alone is not enforcement. When an
agent authenticates directly against a target, the setup verifies who is calling but leaves no point
at which a policy can pause, inspect or require a human decision, so the operation is recorded only
in the target's logs, if at all. The vendor names hallucinated secrets committed to source files,
dependency updates carrying known CVEs, and logic that bypasses existing security controls as the
kinds of thing that reach version control under that arrangement, and argues that a post-hoc
pull-request review is too late because the artifact already exists — potentially exposing secrets
or triggering downstream jobs before a reviewer intervenes.

## Capabilities

The gateway's stated behaviour for a Git push is to intercept it, extract the diff, and check the
configured policy. Where that policy includes [[DefinedTerm/human-in-the-loop]] approval, the diff
is routed to a reviewer's console and the commit is forwarded only after explicit consent. The
session is recorded in full and the approval decision stored alongside it.

Because the gateway is the only component that sees the request, the vendor describes several
controls as available only from that position: inline masking of detected secrets before they reach
the repository, rewriting insecure imports, blocking, and logging every interaction for later
replay. It also holds the credential for the target service itself, so the agent never sees the
underlying secret — which the vendor presents as a reduction in credential-leakage risk rather than
as an access-control change.

Policy is driven by identity. The described setup begins at an identity provider such as Okta or
Azure AD; the agent authenticates over OIDC, and the gateway verifies the token and extracts group
membership and attributes. The worked example restricts requests to agents in an `ai-coding` group
and consent to reviewers in a `code-approval` group.

## Adoption & Ecosystem

hoop.dev is MIT licensed and available on GitHub, so it can be self-hosted inside an organization's
own network and wired to an existing identity provider. The vendor states it works at the protocol
level, so any agent that can speak Git, HTTP or the relevant API can be routed through it, and that
it sits in front of existing CI/CD tooling rather than replacing it — adding approval and audit
without changing the downstream toolchain.

The audit trail is the outcome the vendor puts forward for compliance: session logs, a record of who
approved each change, and the stored masked diff, exportable to meet reporting requirements.
