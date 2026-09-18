---
title: "Qoder"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.12231'
    hash: sha256:08aa95b018a1374f9de491d626d4f394b8efec41d830ef1726a1b8db6a69d9d6
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An AI IDE from Alibaba whose rule files live under `.qoder/rules/`, one of five such tools examined in a 2026 mining and survey study of AI IDE rules."
  applicationCategory: "AI IDE"
  author: "Alibaba"
---

Qoder is an [[DefinedTerm/ai-ide]] published by Alibaba. It is one of the five tools
[[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] selected for study on the basis that each
lets developers explicitly define [[DefinedTerm/ai-ide-rules]] the IDE must follow during code
generation and chat interactions. That study records its release date as 21 August 2025, per the tool's official
changelog.

## Capabilities

Qoder's rule files live under `.qoder/rules/` in the project. Beyond the location and the fact that
rules are honoured during generation and chat, the source used here characterises the mechanism
generically across all five tools rather than describing Qoder's own implementation of it — see
[[DefinedTerm/ai-ide-rules]] for the shared account.

## Adoption & Ecosystem

Two figures from that study bear on adoption, and they measure different things. In its repository
mining, an initial search returned 125 candidate Qoder projects; after keyword and rule-file
filtering and manual inspection, 1 remained in the final dataset of 83 projects declared as
built with an AI IDE. In its practitioner survey, 16 of 99 respondents reported currently using
Qoder for development. The mining figure reflects how many public projects both use the tool and say
so in their README or description, which the study notes undercounts projects that use an AI IDE
without declaring it; the survey figure reflects self-reported use among developers who had committed
changes to rule files.
