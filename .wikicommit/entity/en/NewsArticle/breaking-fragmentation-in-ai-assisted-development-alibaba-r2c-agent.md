---
title: "打破 AI 辅助开发碎片化困境，阿里巴巴 R2C Agent 的 AI 编程实践"
type: "schema:NewsArticle"
lang: en
tags: [end-to-end-ai-development, requirements-to-code, enterprise-ai-adoption]
sources:
  - type: url
    url: 'https://www.infoq.cn/article/26bj1vg2trtwsr96hlwr'
    hash: sha256:e072955ccd8e67cef957e8f47df02d138f12235c05ba907a2d57f8728d2ff37c
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A November 2025 InfoQ China write-up of an AICon 2025 Beijing talk by a senior Alibaba technical expert on R2C Agent, an internal system that aims to support the whole development pipeline with AI instead of isolated coding tools."
  datePublished: "2025-11-12"
  publisher: "InfoQ"
---

The article ("Breaking out of fragmented AI-assisted development: Alibaba's R2C Agent in AI programming practice") is InfoQ's edited transcript of a talk given in June at AICon 2025 in Beijing by a senior technical expert at Alibaba, published on 12 November 2025. The talk presents [[SoftwareApplication/r2c-agent]] — R2C standing for "requirement 2 code" — as the speaker's team's answer to a problem they saw with AI coding tools such as [[SoftwareApplication/cursor]], [[SoftwareApplication/github-copilot]], Bolt.new and [[SoftwareApplication/cline]]: that they are hard to integrate with existing development processes and make collaboration fragmented.

The speaker's argument is that engineers spend only an estimated 30–40% of their time actually writing code, that real projects involve frontend, backend, design and product roles working as a long pipeline, and that an AI tool which excels at one step has its benefit diluted across the whole flow. R2C Agent is described as an attempt to support that pipeline end to end, from requirements and design drafts through to code, review and integration.

## Key Points

- The speaker attributes the AI-programming boom to large capital investment driven by advances in large models, and singles out Claude 3.5 as the release that brought a breakthrough in underlying capability; the advice drawn from this is to avoid building in directions a sudden model advance could overturn.
- The team describes its goal as a third stage beyond code completion and design-to-frontend-code generation: having the model build complete features from whatever the requirement is.
- R2C Agent unifies heterogeneous inputs — market and product requirement documents, technical designs, API test cases, visual and interaction drafts — into an intermediate layer, and treats the whole solution as a matter of keeping prompts and context consistent and understandable to AI.
- An early lesson: relying entirely on AI to generate technical documents did not work well, while having engineers themselves convert requirements into AI-friendly technical documents noticeably improved efficiency and accuracy.
- Execution splits work into sub-tasks coordinated by a main agent, so each sub-task is deterministic and needs no extra planning by the agent; the speaker's view is that for deterministic tasks explicit instructions beat free rein.
- The speaker reports that the adoption rate of AI-generated content across R2C's frontend, backend and testing stages has passed 50% against a 50% target, and that about 60–70% of frontend development work is already covered with high quality; these are the team's own figures, reported in a talk.
- The speaker contrasts "AI DEV" with "AI coding": AI speeds up and changes steps within a software process that remains sound, and coding tools not tied into the existing workflow only deepen fragmentation, at most making individual skilled users stand out without lifting the team.

## Context

The article is a talk transcript lightly edited by InfoQ, so its claims are the speaker's own account of the team's internal system rather than independent reporting. The speaker notes that he knows of no platform that yet delivers "state the requirement and everything else is automated", and recommends that individuals and teams practise hands-on to benefit from AI.
