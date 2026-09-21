---
title: "Devin"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, agent-security]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20260403-secure-devin-management/'
    hash: sha256:bc915a8ef4d5b712d51f417e33760f31692d9d15436252e3de284e4235644d53
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Cognition's autonomous coding agent, cited as an emerging example of goal-agentic (Level 3, SE3.0) AI software engineering that can take a well-defined technical goal and execute a multi-step plan across code, documentation, and other project artifacts. An enterprise operator's account describes it as a service that can autonomously investigate code, write code, and submit pull requests."
  applicationCategory: "Autonomous coding agent"
  author: "Cognition"
---

Devin is Cognition's autonomous coding agent, discussed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] alongside Google's [[SoftwareApplication/google-jules]], OpenAI's Codex, and Anthropic's [[SoftwareApplication/claude-code]] as an example of an agent aiming for Goal-Agentic (Level 3, SE3.0) capability in the paper's [[DefinedTerm/se-autonomy-levels]] hierarchy: taking a well-defined technical goal (e.g. "add a caching layer") and executing a multi-step plan, self-devised or human-guided, across code, documentation, and other essential project artifacts.

A team operating it at Mercari describes it in more workaday terms, as a service that can autonomously investigate code, write code and submit pull requests, and notes that operating it at an organizational level comes with several management challenges ([[BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management]]).

## Capabilities

The paper cites DeepWiki, used by Devin, as an early example of a persistent-memory capability: it lets the agent build and refer to its own documentation and decision logs across multiple tasks, creating continuity and helping prevent it from repeating past mistakes — an example the paper uses to motivate its proposed [[DefinedTerm/ai-teammate-lifecycle-engineering]] activity.

The Mercari account describes the execution model an operator has to work with: Devin launches an independent virtual machine for each session, so in its initial state it holds permissions only for source-code management services such as GitHub, and connecting it to cloud environments or ticket-management services means configuring credentials such as API keys individually. That post also records that members within an Organization can access the file system and shell inside sessions, and that as an AI agent Devin can freely use any API key it is given — two properties it treats as the reason credentials must be handled with care.

Several product surfaces appear in that account. Devin Knowledge is described as functioning similarly to Agent Skills within Devin. Devin MCP is the interface through which agents reach Devin, and requires an API key. Devin Wiki allows retrieval of repository contents and natural-language search through Devin MCP; the post's stated reason for delegating source-code investigation to it is that an AI agent exploring source code directly consumes a large amount of context, which delegating reduces.

## Enterprise Administration

The Mercari post is the fullest description this wiki holds of Devin's administrative surface, and it is written from the operator's side rather than the vendor's. Under the Enterprise plan, multiple Organizations are managed centrally through an Enterprise management layer, rather than sharing a single Organization as on the Core or Team plans — the features that led that team to choose it were SSO through Okta, audit logs, permission management, and environment isolation per team.

Management is exposed through two API versions. The post describes v3 as the latest Enterprise management API, allowing management of Members, Roles, Secrets and Knowledge at both Enterprise and Organization levels, and documented as REST APIs with detailed request and response specifications; it states that Devin released v3 in late 2025 and added Secret management to it in January 2026. That team built its automation on v3 and used the v2 API for API key management alone, v2 allowing creation, retrieval and deletion of API keys across multiple Organizations. It uses the v3 Enterprise Audit Logs endpoint, which it says differs from the v2 endpoint in having pagination.

The post names three things the product did not provide at the time of writing, each of which that team had to build around: there is no official Terraform provider, so it wrote its own using the Terraform Plugin Framework; Devin does not offer expiration management for API keys as a standard feature, so long-lived keys can otherwise remain in each Organization; and Devin has no OIDC token issuance feature that would let it work with Workload Identity Federation, so Google Cloud access requires service account keys. Usage is bounded by ACU (Agent Compute Unit) limits, which that team sets per Organization and per session to prevent unexpected cost overruns. Its overall assessment is that the v3 API already includes the endpoints required for Enterprise administration, while management requirements not covered by standard features had to be supplemented with custom tools.

## Adoption & Ecosystem

[[Organization/mercari]] rolled it out to multiple teams across the company on the Enterprise plan, assigning Organizations by team or purpose so that each team's information stays isolated, and was running more than ten Organizations with a large number of users at the time of that post. That is one company's deployment, reported by the team that administers it.
