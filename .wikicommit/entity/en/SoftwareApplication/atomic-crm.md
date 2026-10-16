---
title: "Atomic CRM"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-harness, harness-engineering, open-source, claude-code]
sources:
  - type: url
    url: 'https://marmelab.com/blog/2026/09/24/the-state-of-ai-harness-engineering-2026.html'
    hash: sha256:6b235f9874e2acd25e233753bd07b55e930baaa9faa7e3f929bdd45c29e53e5c
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "An open-source CRM written in TypeScript by Marmelab that ships a sophisticated agent harness letting non-developers modify the software through a supervised agent pipeline."
  applicationCategory: "Customer relationship management"
  author: "Marmelab"
---

Atomic CRM is an open-source CRM built by Marmelab. Its repository, `marmelab/atomic-crm`, is a
TypeScript project first committed in February 2024. What sets it apart, according to Marmelab, is a
sophisticated agent harness that lets non-developers modify the software through a supervised agent
pipeline. In Marmelab's 2026 survey of harness engineering the CRM is classed as a product-embedded
harness and is one of the 11 harnesses that cleared the survey's filters for testing and iteration, a
placement its own authors ask readers to weigh with that in mind.

## Capabilities

As described in [[BlogPosting/the-state-of-ai-harness-engineering-2026]], the harness consists of 148
harness files, with 77 executable hooks, `deny` rules and 33 tests, the hooks having their own test
suite. It chains seven agent roles, including a reviewer role that Marmelab says often improves the
outcome. The Atomic CRM Builder logs every step of every
session and lets the user parse those logs to understand how skills and tools are used — one of the few
harnesses the survey found recording anything about its own use.

## Adoption & Ecosystem

Marmelab presents Atomic CRM as the harness it measured the field against, and is open about where it
departs from the practices its survey recommends: the harness ships no recorded decisions explaining why
any control exists, so none can be safely removed; it keeps a reviewer role although the literature the
survey cites found a reviewer agent to lower success rates; it chains more agent-to-agent handovers than
the four beyond which a cited operations team saw problems fail; and it requires human review for every
pull request.
