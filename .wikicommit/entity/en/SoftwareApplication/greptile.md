---
title: "Greptile"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, agents, coding-tools]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60882/'
    hash: sha256:7997cccac08ed6a2731d85a3012e81cea6de4b141192497c171f97de0740feb1
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An AI code review service that comments on pull requests, holds a conversation about its findings, and learns from the comments and reactions it receives, generating customization rules from them."
  applicationCategory: "AI code review"
  featureList: "Pull-request review comments; conversational replies on the PR; learning from review comments and reactions; automatic generation of custom review rules"
---

Greptile is an AI code review service used on pull requests. It is described in [[BlogPosting/redesigning-code-review-for-the-ai-era]] as one of three AI reviewers a team ran in parallel alongside GitHub Copilot and [[SoftwareApplication/claude-code-action]], and it is the one that post's author names as a personal preference.

What the post records about it is a set of capabilities that go beyond posting findings: it replies to comments and can be consulted on the pull request, it can discuss design intent, and it learns from the review comments and reactions it receives, generating customization rules from them.

## Capabilities

- Reviews pull requests and posts comments, with the post rating its review quality as high and characterizing it as concentrating on what is critical.
- Supports conversation on the pull request itself: replying to its comments and consulting it is possible, which the post likens to working with a human reviewer, and it can discuss design philosophy.
- Learns from the comments and reactions it accumulates, and automatically generates customization rules from them — one of the things the post's author cites when naming Greptile the author's personal favourite of the three, alongside its ability to reply and be consulted like a human reviewer.
- Rated as simple to set up, with review speed rated moderate against Copilot's fastest and Claude Code Action's slow, and domain understanding described as good.

## Adoption & Ecosystem

The post's team runs it as one of three parallel AI reviewers, a deliberate arrangement while the field is unsettled: the stated aim is to have several models look from different angles for now, with the post saying the team may later evaluate and choose which services to keep using. Within that comparison Greptile and Claude Code Action are the two the team's members reportedly rate highest, with Copilot rated fastest and medium on quality.

The post also records two cautions from its own use: Greptile's rules apply across all repositories, and configuring it for one repository specifically is difficult.

Everything here comes from a single engineering-blog post that uses the tool rather than documenting it, and the comparative ratings are that team's impressions rather than measurements. Nothing about the product's own documentation, pricing or scope was available in this source.
