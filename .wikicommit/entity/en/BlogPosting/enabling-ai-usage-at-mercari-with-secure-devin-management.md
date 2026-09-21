---
title: "Enabling AI usage at Mercari with Secure Devin Management"
type: "schema:BlogPosting"
lang: en
tags: [agents, agent-security, secrets-management, infrastructure-as-code]
sources:
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20260403-secure-devin-management/'
    hash: sha256:bc915a8ef4d5b712d51f417e33760f31692d9d15436252e3de284e4235644d53
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An account from Mercari's AI Security team of scaling Devin Enterprise across more than ten Organizations by building a custom Terraform provider and a set of automated management tools on Devin's v2 and v3 APIs, covering member and permission management, secret rotation, API key lifecycle and auditing."
  author: ["Hiroki Akamatsu"]
  datePublished: "2026-04-03"
  publisher: "[[Organization/mercari]]"
---

This post is about the administrative surface an autonomous coding agent needs once it is deployed organization-wide, rather than about what the agent does. Mercari rolled [[SoftwareApplication/devin]] out to multiple teams across the company, and the post — written by an AI Security engineer, describing work done with the AI Agent Platform team — sets out the tooling built to operate it at that scale. Its stated hope is to serve as a blueprint for securely deploying and operating Devin across an enterprise.

The reason the company is on the Enterprise plan is given as a set of requirements for running a remote-environment AI agent at organizational scale: SSO through Okta, audit logs, permission management, and environment isolation per team. Under that plan, multiple Organizations are managed centrally through an Enterprise layer rather than sharing one, and Mercari assigns Organizations by team or purpose because each team's information must be kept isolated and protected.

Three categories of problem follow from that arrangement past ten Organizations and a large user count, and the post names them directly: assigning members relies on manual operations and tracking who belongs where is difficult; third-party credentials must be configured individually per Organization and rotating them manually is time-consuming; and Devin offers no expiration management for API keys as a standard feature, so long-lived unrotated keys risk accumulating. What changed is that Devin released Enterprise API v3 in late 2025, making most management operations automatable — so the team built an in-house management platform in Go and GitHub Actions.

## Key Points

- The management platform's core is a custom Terraform provider, built with the Terraform Plugin Framework because Terraform is Mercari's standard for infrastructure-as-code and no official Devin provider is available. The post's stated benefit is that managing Devin through IaC inserts PR review into member additions and permission changes and makes the state of Organizations and members visible in code, with `terraform plan` showing who will be added to or removed from which Organization before it happens.
- ACU (Agent Compute Unit) limits are set in the same Terraform definitions to control usage per team: `max_cycle_acu_limit` caps the Organization overall and `max_session_acu_limit` caps a single session, which the post frames as preventing unexpected cost overruns.
- The provider also manages Devin Knowledge, which the post says functions similarly to Agent Skills within Devin. The post identifies a tension its own isolation created: because each team sits in a separate Organization and cannot see the others' usage, sharing practical know-how is difficult, and making Knowledge manageable through the provider is what let that know-how be distributed across teams.
- Secrets are rotated in bulk rather than per Organization. Devin launches an independent virtual machine per session, so connecting to anything beyond source-code management requires credentials configured individually; the post's stated risk is that an AI agent can freely use any API key it is given and that members within an Organization can access the file system and shell inside sessions, so Mercari centrally manages those keys and rotates them at short intervals. The procedure is: the administrator rotates credentials in each service, the new values go into Google Cloud Secret Manager, GitHub Actions triggers the automation, and rotation distributes them to every Organization — with no extra effort when new Organizations are created.
- Google Cloud service account keys are handled as a deliberate exception. Devin has no OIDC token issuance feature that would let it use Workload Identity Federation, so service account keys are required; Mercari otherwise prohibits issuing them company-wide through Organization Policy, and the answer was a dedicated Google Cloud project excluded from that policy with `iam.serviceAccountKeyExpiryHours` as a compensating control, so keys are automatically disabled after a fixed period even if the automation stops.
- Audit logs are pulled through the v3 Enterprise Audit Logs endpoint — chosen over the v2 endpoint because it has pagination — by a Cloud Run Job that forwards new logs to a PubSub topic, from which they are analysed and stored in BigQuery. This integration with the in-house security monitoring platform is credited to a colleague working with the Threat Detection and Response team, and audit logging is named as one of the requirements for adopting Devin Enterprise in the first place.
- API key expiration is enforced by automation because Devin does not provide it: a job retrieves all keys across the Enterprise and invalidates any that have exceeded a set age. The post's stated motivation is that these keys are primarily used to reach Devin MCP, through which source code can be obtained indirectly, and that in environments with multiple agents credentials can linger in the configuration of unused agents or be set as a personal key in a custom agent shared internally.
- Devin Wiki runs in its own Organization, separate from the per-team development Organizations, and allows repository-content retrieval and natural-language search through Devin MCP. The post's stated reason for delegating source-code exploration to it is context economy: an AI agent exploring source code directly consumes a large amount of context. Because the expiry automation would invalidate the keys internal agents need, a further automation recreates those keys at short intervals and stores them in Google Cloud Secret Manager, with access granted to named agent service accounts through Terraform.
- Everything runs on GitHub Actions rather than on Google Cloud, and the post gives maintenance as the reason: automation in the repository runs without deployment, holding no cloud resources keeps costs low and reduces the mental burden during handoffs, and long-term maintenance through organizational change argues for small dependencies. Scheduled runs are supplemented by `workflow_dispatch` for immediate rotation in emergencies. Because Actions can be run freely, the team strictly configures permissions and branch protection, and uses Google Cloud Workload Identity Federation to reach service accounts and Secret Manager.
- Only API key management uses the v2 API; the v3 API covers members, roles, secrets and knowledge at both Enterprise and Organization levels. The post reports the v3 API as already including the endpoints required for Enterprise administration, and states an intention to keep automating safe management of a wider range of resources as Devin's capabilities expand.

## Context

The post is written from the position of an operator rather than a vendor, and most of what it describes exists because a standard feature does not: the Terraform provider because no official one is available, the key expiry job because Devin offers no expiration management, the service-account-key exception because Devin cannot issue OIDC tokens. Its framing throughout is that the Enterprise plan's management requirements could not be covered by standard features alone and were supplemented with custom tools.

It reports no measurement of the outcome, describing instead what was previously manual and is now automated. The post refers to Devin's official API documentation and to Google Cloud's own best-practice guidance for service account keys as the basis for particular choices, and to an earlier post on the company's detection engineering platform, but describes none of them beyond the role each plays in its own account.
