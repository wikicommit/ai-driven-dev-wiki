---
title: "Windsurf"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.12231'
    hash: sha256:08aa95b018a1374f9de491d626d4f394b8efec41d830ef1726a1b8db6a69d9d6
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html'
    hash: sha256:7ea8a1ed00a8a82a1cd5c918dc9ccc8a4e1c4ff443010387ad6a0351210ba291
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An AI IDE from Codeium whose rule files live under `.windsurf/rules/`, one of five such tools examined in a 2026 mining and survey study of AI IDE rules."
  applicationCategory: "AI IDE"
  author: "Codeium"
---

Windsurf is an [[DefinedTerm/ai-ide]] published by Codeium. It is one of the five tools
[[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] selected for study on the basis that each
lets developers explicitly define [[DefinedTerm/ai-ide-rules]] the IDE must follow during code
generation and chat interactions. That study records its release date as 13 November 2024, per the tool's official
changelog.

## Capabilities

Windsurf's rule files live under `.windsurf/rules/` in the project. It also supported a single-file `.windsurfrules` format, which was later superseded by the directory-based mechanism. Beyond the location and the fact that
rules are honoured during generation and chat, the source used here characterises the mechanism
generically across all five tools rather than describing Windsurf's own implementation of it — see
[[DefinedTerm/ai-ide-rules]] for the shared account.

## Adoption & Ecosystem

Two figures from that study bear on adoption, and they measure different things. In its repository
mining, an initial search returned 3684 candidate Windsurf projects; after keyword and rule-file
filtering and manual inspection, 5 remained in the final dataset of 83 projects declared as
built with an AI IDE. In its practitioner survey, 23 of 99 respondents reported currently using
Windsurf for development. The mining figure reflects how many public projects both use the tool and say
so in their README or description, which the study notes undercounts projects that use an AI IDE
without declaring it; the survey figure reflects self-reported use among developers who had committed
changes to rule files.

A practitioner's account of using it, [[BlogPosting/assessing-internal-quality-while-coding-with-an-agent]],
describes adding a feature to an existing Swift Mac application with Windsurf and Sonnet 3.5, asking it
for a plan for each chunk of work before the implementation. Its author found that the combination sped
up writing code but required careful planning with prompts and constant switching between Windsurf and
Xcode for building, testing and debugging, that the generated code had significant quality issues, and
that the agent tended to get stuck trying to fix a problem — so that on the whole he did not feel he was
getting much out of it. In the same account, a later attempt with [[SoftwareApplication/claude-code]] and
Sonnet 4.5 went better enough for him to adopt that tool regularly.
