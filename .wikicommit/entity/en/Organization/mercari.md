---
title: "Mercari"
type: "schema:Organization"
lang: en
tags: [ai-adoption, industry, agent-security]
sources:
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20251030-taming-agents-in-the-mercari-web-monorepo/'
    hash: sha256:2be25eae3259d1a99d5bcb659f731c2564ffe64e94c6bf0ad803148e7fb2a464
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20260403-secure-devin-management/'
    hash: sha256:bc915a8ef4d5b712d51f417e33760f31692d9d15436252e3de284e4235644d53
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A company reported by its own engineers as adopting AI-Native development principles — one team's account describes engineers empowered to choose their own AI tools rather than standardizing on one — and as running an AI agent service across more than ten internal Organizations under a centrally administered enterprise plan."
---

Mercari appears in this wiki as an adopter of AI-driven development practice rather than as a vendor of tooling. What is recorded here comes from posts on the company's own engineering blog, so it establishes how its engineers describe the organization rather than an outside assessment of it.

The organization-level stance one of those posts describes is a deliberate refusal to standardize. As the company adopts what the post calls AI-Native development principles, everyone was empowered to adopt tools of their choosing and given resources to try out new technology; the stated goal was to let engineers use these tools without forcing them into a completely different setup. The post reports the cost of that freedom as well as its benefit: the team learned about a broad range of tools quickly, while the efficacy of those tools and the shape of their output varied greatly, even within teams.

A second post describes a separately administered part of the same picture: the company operates an AI agent service under an enterprise plan in which Organizations are assigned by team or purpose, on the stated grounds that Mercari has numerous teams spanning multiple business domains and the information each handles must be kept isolated and protected. That post does not refer to the tooling the first one describes, and neither presents the two as one policy.

## Structure

Several internal groups are named across these posts, which state no count of them. The Web team, described as made up of people from diverse backgrounds whose tools and setups differ widely, has been building Mercari's new Global App; its monorepo follows a modular approach, organized as pnpm workspaces with module boundaries enforced in tooling. The AI Security team worked together with the AI Agent Platform team on the agent-administration platform described below. The integration that feeds that service's audit logs into the company's in-house security monitoring platform is credited to Anna from AI Security and Threat Detection and Response — wording that leaves it open whether one team is meant or two.

The second post also gives some of the company's engineering defaults, as constraints its own work had to fit: Terraform is the standard tool for infrastructure-as-code resource management and engineers work with it daily; Go is widely used within the company; and Google Cloud is the primary cloud, with Organization Policy prohibiting the issuance of service account keys across the board, following Google Cloud's official best practices — a prohibition that same post then works around with a dedicated project excluded from the policy and key expiry as a compensating control.

## Activities & Products

Among the tools most popular in the Web team, the first post names Cursor, [[SoftwareApplication/claude-code]], GitHub Copilot and, more recently, Codex CLI. That team's response to the divergence between their respective rule formats was to consolidate on [[DefinedTerm/agents-md]] as a single source of truth — the account of that consolidation is on [[BlogPosting/taming-agents-in-the-mercari-web-monorepo]]. The same post states an intention to share the team's learnings across Mercari and to inspire other teams exploring AI-Native development, which places that practice as one team's rather than the company's settled standard.

Separately, [[SoftwareApplication/devin]] has been rolled out to multiple teams across the company, with more than ten Organizations and a large number of users at the time of writing. The AI Security team, working with the AI Agent Platform team, built an in-house management platform in Go and GitHub Actions on top of Devin's Enterprise APIs, covering member and permission management, secret rotation, API key lifecycle management and auditing — the account of that work is on [[BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management]].
