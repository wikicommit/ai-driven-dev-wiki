---
title: "WINTICKETで仕様書作成にAIが定着するまでにやったこと"
type: "schema:BlogPosting"
lang: en
tags: [specification-writing, ai-adoption, industry]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62048/'
    hash: sha256:b4ce4f9f18062c39d2f2b84a6b23e1c90c1bde712602bfa93006cf4549c21e28
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A CyberAgent Developers Blog post on how the WINTICKET team got AI-assisted specification writing adopted, so that 33 of the 36 specifications written over two months were written together with AI."
  author: ["ostk0069"]
  datePublished: "2026-02-10"
  publisher: "[[Organization/cyberagent]]"
---

This post, written by an engineer at WinTicket and published on the CyberAgent Developers Blog, describes how
the team behind WINTICKET, a betting service for keirin and auto racing, made AI a settled part of writing
specifications. It reports that between December 2025 and January 2026, 36 specifications were written and 33
of them (92%) were written together with AI: 20 of 21 requirements specifications and 13 of 15 development
specifications.

The author's central claim is that what decides the outcome is not the AI's accuracy — a model of reasonable
quality is enough — but two other things: putting into words what an ideal specification is for this product
and having the AI read it, and fitting the tool to the people who will actually write specifications so that
an AI setup is not built and then left unused. The post walks through how the team defined its ideal
specifications, chose and configured its tool, and kept it in use.

## Key Points

- The initiative began in September 2025; its goal as of February 2026 was for AI to reliably produce a
  specification scoring 80 out of an ideal 100, much faster than a person could, rather than aiming for 100,
  because the context needed for development is not fully captured as data and people's understanding of AI
  varies.
- Anyone at WINTICKET can propose and run an initiative, so people from business, engineering and design who
  had never written a specification often had to, while the organization had no written definition of a good
  specification and no onboarding for writing one.
- WINTICKET uses two kinds of specification: a requirements specification, written by anyone at the planning
  stage to answer why and what, for the business owner's go decision; and a development specification, written
  with engineering and design to answer how, at a level that can be implemented.
- The team defined each document's structure by asking its consumers — designers, engineers, QA and data
  management — what they needed, which produced requirements such as stating KPIs up front, covering error
  handling and edge cases, and laying out state-dependent behaviour as MECE Markdown tables.
- Development specifications record only the specification (what), never implementation details (how), and
  ban vague Japanese expressions such as "for a while" or "basically".
- After evaluating Dify, n8n, ChatGPT, Claude, Cursor and [[SoftwareApplication/devin]], the team chose Devin
  because it could be invoked from Slack with no new tool to learn, held a dialogue in a Slack thread, reached
  Kibela documents through [[DefinedTerm/model-context-protocol]] servers, and read the app, web and backend
  repositories through [[SoftwareApplication/deepwiki]].
- A Slack Workflow form that must be completed before Devin starts collects the initiative's name, summary,
  background, goals and KPIs, affected areas and what is out of scope, after which Devin asks follow-up
  questions in the thread.
- Separate Devin Playbooks (system instructions) for the two document types drive information gathering,
  investigation of existing behaviour through [[SoftwareApplication/ragent]] and DeepWiki, cost-benefit
  analysis or dialogue-based detailing, and a checklist-based quality check before the result is posted to
  Kibela.
- The author attributes adoption to three things: defining the ideal specification, minimizing learning cost,
  and having a few people try the tool first while improving the Playbooks through a Slack feedback channel.
- A follow-up mechanism lets a team member add a specific emoji reaction to a Slack thread about a
  specification; a Slack App then starts Devin with an update Playbook, which identifies the target document
  from the channel name and conversation and updates it through the Kibela MCP server.

## Context

The post is a firsthand report from one product team, and its adoption figures and lessons describe that team
alone. Its conclusion is that AI-assisted specification writing needs no advanced technology, only an
organization that has articulated its ideal specification and a tool offered in a form its actual writers find
easy to use. It sits among other CyberAgent accounts of AI adoption on this wiki and relates to
[[DefinedTerm/spec-driven-development]], although the post itself does not use that term.
