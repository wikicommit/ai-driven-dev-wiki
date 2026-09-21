---
title: "Zalando"
type: "schema:Organization"
lang: en
tags: [enterprise-adoption, developer-platform]
sources:
  - type: url
    url: 'https://engineering.zalando.com/posts/2026/08/agentic-engineering-at-zalando-a-snapshot.html'
    hash: sha256:33171882bb4809ae93923b09f4e1fe6315bf6de5690393243df5a995118678bc
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A company whose engineering organization — described as more than 250 teams across several business lines — has published a firsthand account of adopting agentic engineering at scale, built around an internally hosted multi-provider LLM proxy and a deliberate refusal to standardize on a single coding tool."
---

Zalando appears in this wiki as the subject of its own published account of agentic engineering
practice. That account describes an engineering organization of more than 250 teams innovating
across the company's business lines, with large language models delivering value in different
forms and at different paces across them. A later section of the same account gives the figure as
more than 200 teams; the source states both and reconciles neither.

The engineering estate, as described there, is largely built from separate repositories for
microservices rather than monorepos, though the company operates a few — including a Zalando web
monorepo that sets up a deployment for each pull request, wired to live data. It runs a
Backstage-based developer portal called Sunrise and publishes a Tech Radar, to which an internal
AI section has been added.

## Activities & Products

What this wiki's source establishes about Zalando concerns its internal engineering platform. Its
ML platform team deployed a [[SoftwareApplication/litellm]]-based API proxy in January 2024,
providing API access to models from OpenAI, AWS Bedrock and Google Vertex. The team reports serving
2,000 monthly active users from six pods of two CPU cores and 4 GB of memory each — a footprint the
account presents as the result of enforcing proxy restarts after 20,000 requests to mitigate
LiteLLM's stability and memory leak issues, rather than as an unconditional capacity figure. The
proxy is complemented by a chat UI — a fork of a since-unmaintained open source codebase — and a
custom CLI tool built with pydantic-ai, which originated in an August 2024 hackathon before coding
agents existed and later attracted a small community of maintainers who extended it with an
interactive mode, agent mode with MCP support, an HTTP-to-stdio MCP proxy, and a command that
installs safe coding-agent configurations.

Beyond the platform itself, the account describes a risk-based pull-request approval bot that
auto-approves the 33% of PRs it classifies as low risk, a centralized collection of
[[DefinedTerm/agent-skills]] distributed as plugins, and an agent platform under construction that
composes open source components — including kagent for Kubernetes runtime concerns — alongside an
Identity Broker for delegation chains and on-behalf-of flows between agents and MCP servers.

Its knowledge-sharing formats are described in the same detail: an LLM guild, whose chat channel
the account dates to 2024 and whose knowledge-sharing sessions run weekly for an hour; topic-driven
hackathons of two to three days; on-site *GenAI Labs* sessions for around 20 people; and monthly
trainings on using MCP servers and building agents with pydantic-ai, whose trainers are recruited
from earlier Lab attendees. The company also runs an annual Software Engineering Community
Conference, where it deliberately balanced an Agentic Engineering track on day one against an
Engineering Fundamentals track on day two.

For the company's own retrospective on all of this, see
[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]].
