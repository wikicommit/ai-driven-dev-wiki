---
title: "R2C Agent"
type: "schema:SoftwareApplication"
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
  description: "An internal Alibaba agent (R2C, \"requirement 2 code\") that drives the development pipeline from a knowledge base, DingTalk documents and design drafts, aiming at end-to-end AI support rather than isolated AI coding tools."
  applicationCategory: "Requirements-to-code AI development agent"
  featureList: "Unified intermediate layer for requirements, technical designs, API test cases and visual/interaction drafts; VS Code plugin agent that reads requirement documents through browser automation under the developer's own permissions; MCP service and defined workflows; main-agent coordination of deterministic sub-tasks"
  author: "Alibaba"
---

R2C Agent — "R2C" standing for "requirement 2 code" — is the internal name of an AI programming system built by a team at Alibaba and presented at AICon 2025 in Beijing, as reported in [[NewsArticle/breaking-fragmentation-in-ai-assisted-development-alibaba-r2c-agent]]. It is described as driving the whole development pipeline from a knowledge base, DingTalk documents and design drafts, with the goal of end-to-end AI support for development regardless of which platform or IDE each participant uses.

It grew out of the team's view that AI coding tools are hard to integrate with existing development processes and make collaboration fragmented, so that a tool that does well at one step of a long, multi-role pipeline delivers diluted benefit overall. A consistent experience for everyone involved — frontend, backend and test engineers using different IDEs and platforms — is described as the team's first and most important aim.

## Capabilities

R2C Agent's framework unifies its inputs — market and product requirement documents, technical designs, API test cases, visual drafts and interaction drafts — into an intermediate layer, and abstracts the end-to-end solution into two elements, prompts and context, which that layer keeps consistent and understandable. The team focuses on four things: a domain knowledge base, project documents, design drafts, and their structured expression, which may be structured or unstructured as long as AI can readily understand it. Design drafts are turned into a semantic representation of their design elements that large models can understand well.

Lacking supporting infrastructure at first, the team built it as a VS Code plugin agent. Requirement documents kept in DingTalk Docs, Yuque or Word are read by the agent driving a browser in an RPA-like way, which lets it read any document the developer has permission to access. The implementation publishes its own MCP ([[DefinedTerm/model-context-protocol]]) service and organizes requirement documents, API documents, technical documents, the business knowledge base and a visual library through defined workflows into an iterative development flow.

Its customization concentrates on three points: managing the context window by giving the model only the content a task needs, running main tasks and sub-tasks independently, and having the main task manage while sub-tasks implement. Splitting work into sub-tasks coordinated by one main agent keeps each sub-task deterministic, so the agent needs no additional planning and is kept from running out of control.

## Adoption & Ecosystem

Version 1.0 went live in mid-May, ahead of the June talk, covering the flow from interaction and visual drafts to technical designs, API documents and test cases; the speaker reports that frontend code reproduced designs closely, including integration against the API and technical documents, leaving frontend engineers little more than "filling in the blanks". The team reports that across R2C's frontend, backend and testing stages the adoption rate of AI-generated content has passed 50%, and that in frontend work a component-to-code step (C2C), which reuses previously written components and code, already covers roughly 60–70% of development work with high quality. These figures are the team's own, given in a conference talk. Its builders learned that engineers writing AI-friendly technical documents themselves worked far better than having AI generate those documents, and they treat document management as the most important part of implementing the approach.
