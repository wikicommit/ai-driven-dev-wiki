---
title: "Shift Left & Right: Wie KI-Integration über das Coding hinauswächst"
type: "schema:BlogPosting"
lang: en
tags: [devops, specification, production-feedback, ai-integration]
sources:
  - type: url
    url: 'https://www.codecentric.de/wissens-hub/blog/shift-left-and-right-wie-ki-integration-ueber-das-coding-hinauswaechst'
    hash: sha256:c56eb7ca57b7c6a3d943d7e214b28e500b4b15141ffd4b5854443353c81b9ebc
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The closing post of a German-language codecentric series on AI integration, arguing that faster AI code generation shifts the bottleneck to the specification before coding (Shift Left) and to verification and learning in production after it (Shift Right)."
  author: ["Marc Pudelski"]
  datePublished: "2026-09-04"
  publisher: "codecentric AG"
---

This German-language post closes a codecentric series whose earlier episodes dealt with making AI integration work inside the coding loop. Its starting claim is that technical code generation is only one side of the story: the drastic acceleration of code generation puts heavy pressure on the rest of the system. On the left side, requirements definition faces the question — in ever shorter cycles — of what exactly should be built and whether it is the right thing; on the right side, there is pressure to check the rapidly produced results in practice just as quickly and reliably. The post argues that unless both edges are mastered, any speed gained is lost inside the coding silo.

It defines [[DefinedTerm/shift-left]] as ensuring quality and clarity earlier in the development lifecycle, with the specification as the decisive lever, and [[DefinedTerm/shift-right]] as moving quality gates and test execution into the real runtime context. It notes that both concepts come from the DevOps and product world, and argues that AI amplifies both — which is why, on its account, using AI only in the coding loop leaves much of its potential unused and creates new bottlenecks.

## Key Points

- AI acts on the specification at two levels, the post says: manually written specs can be checked with AI support, and AI can also actively complete requirements, point out contradictions and propose suitable test cases.
- On the operations side, it says, AI scales work that used to be manual: auto-triage, log analysis and pattern recognition now run automatically.
- The post reports that in practice the distribution of working hours changes: spec engineering, specification as a discipline of its own, takes up much more room while the pure coding share shrinks noticeably.
- It argues that engineers, designers and product managers increasingly grow into one another's tasks, with developers taking on responsibility in requirements engineering and design because the higher speed demands parallel work.
- It gives one anonymised example from an insurance customer project: after a one-off two-week setup for LLM-supported spec reviews, coding-loop iterations per feature fell on average from 4.2 to 2.1.
- It answers the objection that more specification sounds like waterfall: Shift Left means sharpening the specification for the next coding cycle before entering it, refined continuously rather than fixed once at the start.
- It says AI support for production — auto-triage, root cause analysis, anomaly detection and auto-remediation such as a rollback on performance drops — is technically available today but used by few teams, not for lack of technology but because no concrete pipeline steps have been built for it.
- In the experience the post reports, most AI initiatives fail at Shift Right because learning loops are not structurally anchored — there is no regular forum for evaluating production data and no rhythm that turns incident trends into roadmap changes — producing what the post calls "Shift-Right theatre": the data exists but is not used.
- It rates the maturity of both movements in Germany as just emerging.

## Context

The post argues that the two movements together form a closed learning system — Shift Left sharpens the picture of what should be built, Shift Right brings back whether what was built works in practice — and that establishing only one side means going in circles. It presents both as necessary preconditions for making AI integration sustainably useful, and says both require new roles, adapted infrastructure and new working rhythms. It also distinguishes Shift Right, which it treats as purely technical safeguarding, from a product-level learning loop that asks whether the right problem is being solved for the user. The post ends by inviting organisations to contact codecentric for help, and recommends further reading from Red Hat, Sequoia Capital and Codacy.
