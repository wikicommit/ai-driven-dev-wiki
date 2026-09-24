---
title: "Mercari"
type: "schema:Organization"
lang: en
tags: [ai-adoption, industry, agent-security, spec-driven]
sources:
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20251030-taming-agents-in-the-mercari-web-monorepo/'
    hash: sha256:2be25eae3259d1a99d5bcb659f731c2564ffe64e94c6bf0ad803148e7fb2a464
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20260403-secure-devin-management/'
    hash: sha256:bc915a8ef4d5b712d51f417e33760f31692d9d15436252e3de284e4235644d53
  - type: url
    url: 'https://engineering.mercari.com/blog/entry/20251201-pj-double-towards-ai-native-development/'
    hash: sha256:759a8657a3547ccd879fd3b7b260a4e7eda5e4cbc7fbb559a4b86aabecb602c4
  - type: url
    url: 'https://engineering.mercari.com/blog/entry/20251225-mercari-ai-native-company/'
    hash: sha256:ed22a2b68e6e9e11d985d3ca79f7337bec6642349f4634d9b3bf2e9810a83cae
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A company that has declared the goal of becoming an AI-Native Company — rebuilding its products, ways of working and organization around AI — and whose engineers describe both team-level freedom to choose AI tools and a company-wide effort, launched in July 2025, to standardize an AI-Native development process; it also runs an AI agent service across more than ten internal Organizations under a centrally administered enterprise plan."
---

Mercari appears in this wiki as an adopter of AI-driven development practice rather than as a vendor of tooling. What is recorded here comes from posts on the company's own engineering blog, so it establishes how its engineers describe the organization rather than an outside assessment of it.

The stance one of those posts describes is a deliberate refusal to standardize on a single tool. As the company adopts what the post calls AI-Native development principles, everyone was empowered to adopt tools of their choosing and given resources to try out new technology; the stated goal was to let engineers use these tools without forcing them into a completely different setup. The post reports the cost of that freedom as well as its benefit: the team learned about a broad range of tools quickly, while the efficacy of those tools and the shape of their output varied greatly, even within teams.

A second post describes a separately administered part of the same picture: the company operates an AI agent service under an enterprise plan in which Organizations are assigned by team or purpose, on the stated grounds that Mercari has numerous teams spanning multiple business domains and the information each handles must be kept isolated and protected. That post does not refer to the tooling the first one describes, and neither presents the two as one policy.

A third post, from Merpay's VP of Engineering office, describes a company-level effort to standardize something different: not the tools engineers use but the development process, which it explicitly wants to be independent of any particular tool. It recounts that in early 2025 AI tools and MCP servers were adopted bottom-up, each developer exploring their own methods — a phase it calls "Divergence" — and that while some developers became dramatically more productive, a gap opened between those who could use AI well and those who could not, and the shared practice stayed at the level of local tips and shared `CLAUDE.md` or Cursor Rules files. Its response was Project Double (pj-double), launched around July 2025 with the mission of doubling product-development productivity, which set out to move to a "Convergence" phase: a company-wide standard development process that reproduces high productivity. The three posts describe different teams at different moments, and none of them reconciles its account with the others.

A fourth post, by the company's CTO, sets these efforts in a company-wide frame. It quotes the president's declaration that Mercari will rebuild its products, ways of working and organization around AI in order to become an "AI-Native Company", and reports that 95% of employees use AI tools, that AI accounts for about 70% of code generation and that development speed rose 64% year on year — while stating that the company does not yet regard itself as AI-Native, because coding productivity alone does not raise the productivity of the whole organization. The same post describes the tool divergence from the company level: Cursor was first rolled out company-wide, then newer coding assistants such as Claude Code appeared and engineers came to use different tools, which made best practices hard to consolidate. Its account of the response is on [[BlogPosting/choosing-ai-native-mercari-guiding-principles]].

## Structure

Several internal groups are named across these posts, which state no count of them. The Web team, described as made up of people from diverse backgrounds whose tools and setups differ widely, has been building Mercari's new Global App; its monorepo follows a modular approach, organized as pnpm workspaces with module boundaries enforced in tooling. The AI Security team worked together with the AI Agent Platform team on the agent-administration platform described below. The integration that feeds that service's audit logs into the company's in-house security monitoring platform is credited to Anna from AI Security and Threat Detection and Response — wording that leaves it open whether one team is meant or two.

The second post also gives some of the company's engineering defaults, as constraints its own work had to fit: Terraform is the standard tool for infrastructure-as-code resource management and engineers work with it daily; Go is widely used within the company; and Google Cloud is the primary cloud, with Organization Policy prohibiting the issuance of service account keys across the board, following Google Cloud's official best practices — a prohibition that same post then works around with a dedicated project excluded from the policy and key expiry as a compensating control.

## Activities & Products

Among the tools most popular in the Web team, the first post names Cursor, [[SoftwareApplication/claude-code]], GitHub Copilot and, more recently, Codex CLI. That team's response to the divergence between their respective rule formats was to consolidate on [[DefinedTerm/agents-md]] as a single source of truth — the account of that consolidation is on [[BlogPosting/taming-agents-in-the-mercari-web-monorepo]]. The same post states an intention to share the team's learnings across Mercari and to inspire other teams exploring AI-Native development, which places that practice as one team's rather than the company's settled standard.

pj-double began by working with more than 30 backend projects at Merpay and Mercari Mobile for three months, tracking their use of AI in weekly meetings, and on the strength of that proposed [[DefinedTerm/agent-spec-driven-development]] (ASDD) in September 2025 — a method in which agents generate an implementation plan and then implement against it. From October 2025 the project grew from one person to a team of more than ten and extended from part of Merpay to the whole company, and from backend design and implementation to requirements, design, iOS and Android client development and QA. The account of that project, including where ASDD fell short, is on [[BlogPosting/pj-double-mercari-development-productivity]]. To track whether faster delivery is costing quality, the team reports monitoring revert rate and MTTR with DX, the developer-experience tool the company has adopted. The CTO's post describes ASDD as the core of the company's development process and names the Double project's aim as doubling productivity.

Two company-wide efforts sit alongside it in the CTO's account. A knowledge-management effort is consolidating information in Notion as a central knowledge base, so that decision history and other context are available to AI agents. An AI Task Force, started in July 2025, divided the company into 33 domains, each with one or two engineers, one or two project managers and a domain owner, and grew to about 100 members. By the end of 2025 it had inventoried about 4,000 workflows across those domains and drawn up roadmaps for converting them to AI. The same post names other agent projects: PJ Socrates, an agent for business-intelligence work that retrieves and analyses internal data on natural-language requests, and PJ Aurora, which generates UI using the company's in-house design system.

Separately, [[SoftwareApplication/devin]] has been rolled out to multiple teams across the company, with more than ten Organizations and a large number of users at the time of writing. The AI Security team, working with the AI Agent Platform team, built an in-house management platform in Go and GitHub Actions on top of Devin's Enterprise APIs, covering member and permission management, secret rotation, API key lifecycle management and auditing — the account of that work is on [[BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management]].
