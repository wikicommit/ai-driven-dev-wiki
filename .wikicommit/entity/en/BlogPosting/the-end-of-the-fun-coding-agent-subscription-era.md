---
title: "楽しかったコーディングエージェントサブスク時代の終わり"
type: "schema:BlogPosting"
lang: en
tags: [pricing, agents, enterprise-adoption]
sources:
  - type: url
    url: 'https://zenn.dev/tkithrta/articles/0378bc53599fb3'
    hash: sha256:ce4c3c894d084c4d3fbc47b8d21cfb386a2dcf6f1d742bfe8f75e4f62c970447
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An opinion piece arguing that pricing for AI coding agents is moving from flat per-user subscriptions to mixes of seat fees, included allowances, credits and token-based metering, comparing how OpenAI Codex, Claude Code and GitHub Copilot bill for agent use as of May 2026."
  author: ["黒ヰ樹"]
  datePublished: "2026-05-29"
---

This post argues that the pricing of AI coding assistance has stopped being a simple "so much per
user per month" subscription. Drawing on vendors' public documentation from 2 April to 29 May 2026,
it describes a shift toward models that combine seat fees, included usage allowances, credits, token
consumption and organization-level budgets and caps, and contends that coding agents in particular
have taken on the character of metered API billing.

Its explanation is structural. Autocompletion returns short outputs for short contexts, whereas a
coding agent reads a repository, explores several files, runs tests, fixes failures and explains its
diff, sometimes calling the model for tens of minutes or hours on one task. A single request from the
user's point of view can therefore consume large and highly variable amounts of input, output and
cached tokens, which the author argues makes unlimited flat-rate plans hard to sustain across light
and heavy users alike.

The post then compares three products and turns to what organizations should check when adopting
them, concluding that coding agents must be managed both as developer tools and as consumers of the
organization's compute — a FinOps concern.

## Key Points

- For [[SoftwareApplication/openai-codex]], the post reports that ChatGPT Business distinguishes a
  fixed-price standard seat from a usage-based Codex seat that draws on workspace credits, and that
  from 2 April 2026 Codex pricing changed from per-message charges to API-token usage, with credit
  rates defined per million input, cached-input and output tokens. It also notes that ChatGPT plans do
  not include API access, which is billed separately.
- For [[SoftwareApplication/claude-code]], it cites Anthropic's documentation as stating that usage is
  billed by API token consumption: Pro and Max plans include an allowance, with standard API rates
  applying once API credits are used beyond it; Team plans combine seat fees, usage limits and optional
  usage credits; and Enterprise seat fees cover platform access only, with usage billed separately at
  standard API rates.
- For [[SoftwareApplication/github-copilot]], it reports that Copilot Business and Enterprise move to
  usage-based billing from 1 June 2026 in a unit called GitHub AI Credits (one credit being US$0.01),
  converted from token usage by model. Monthly allowances of 1,900 and 3,900 credits per user
  respectively are pooled across the organization rather than held per user, and code completion and
  Next Edit Suggestions are stated not to consume credits.
- Set side by side, the post argues, the three differ in detail but share one direction: SaaS seat
  pricing for the base product, combined with credit or token metering for heavy use.
- It proposes five questions for enterprise adoption: what a fixed fee actually includes; what happens
  when a limit is reached (blocking, a cheaper model, or paid continuation); whether allowances are
  pooled across the organization or held per person; whether usage can be audited, made visible and
  capped by user, organization or project; and whether API-based use (custom tools, agents in CI, or
  third-party agents driven by an API key) is budgeted separately from SaaS seats.
- The author reads the move to API-like pricing as a sign of pricing power rather than only of high
  cost: because coding agents enter the daily work of well-paid engineers, companies keep paying near
  API-equivalent costs for them. This interpretation is presented as the author's own, prompted by a
  third party's comment that these vendors have found product–market fit.
- It suggests questions organizations will need to answer, such as AI cost per pull request, time saved
  compared with manual work, which tasks justify expensive models, and how to set per-user caps, and
  compares the shift to the earlier move from owning servers to metered cloud billing.

## Context

The post states that pricing, plan names and included allowances change frequently and tells readers
to confirm current terms on each vendor's official pages; its figures describe the situation as of
late May 2026. It explicitly leaves Google's agent offering out of the comparison as less directly
comparable. Its argument concerns enterprise purchasing and budget control rather than individual
developers, whose experience of paying for a personal subscription it acknowledges may still feel
close to the old flat-rate model.
