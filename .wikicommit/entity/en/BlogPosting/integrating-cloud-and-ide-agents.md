---
title: "云端与 IDE 智能体整合：解决工具碎片化，实现 AI 全流程自动编码"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agent-architecture, coding-tools, ai-adoption]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/hybird-agents-build-ide-intelli-with-cloud-agent/'
    hash: sha256:865ae6df41b7d6f93ed92ec6423a7d6c9755713fef7d9af4b6743f0723d45619
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A September 2024 Chinese-language blog post by Phodal Huang arguing that AI-assisted development tools have become fragmented and proposing collaboration between cloud agents and IDE agents to automate the whole development process, illustrated with the agent language Shire."
  author: ["Phodal Huang"]
  datePublished: "2024-09-07"
---

This post, written in Chinese by Phodal Huang, starts from a view the author says he has stated before: that AI
assistance is moving from helping individual developers to covering the whole software development lifecycle,
which spans requirements analysis, design, development, testing and deployment. The question he poses is how to
break down the barriers between AI-assisted development tools so that they work together.

His answer is collaboration between cloud agents and IDE agents: an agent orchestration system on the IDE side
that works together with agents in the cloud to automate the whole development process. He illustrates it with
[[ComputerLanguage/shire]], an AI coding agent language.

## Key Points

- The author describes the prevailing approach as adding AI to existing DevOps tools and platforms to provide
  scenario-specific agents for end-to-end workflows and multi-role collaboration.
- He argues that the "quick-win and high-leverage" areas his team had recommended enterprises focus on — such as
  assisting structured requirements, code generation and code review — have already been picked, with many
  enterprises having their own tools in pilots, while long-tail areas such as deployment and operations are
  still immature and not necessarily more cost-effective.
- He argues that AI platforms and tools are becoming more fragmented: enterprises buy tools such as GitHub
  Copilot, Tongyi Lingma or CodeGeeX, or build their own on open-source software such as Dify, AutoDev, Continue
  or assorted chatbots, leaving tools scattered across teams that duplicate work and struggle to cooperate.
- He cites examples of IDE agents — Bloop, Tabnine's Jira-to-code feature and GitHub Copilot Workspace — and
  says what they share is combining IDE context obtained through the toolchain with cloud knowledge bases.
- He distinguishes two kinds of IDE-side agent capability: local agents, which are fast because they read local
  context directly but cannot reach cloud knowledge bases, and integration with cloud agents or agent
  marketplaces, which can bring in domain knowledge for tasks such as generating code from requirements or code
  review.
- He argues that development agents depend on one another — a requirements assistant, for instance, needs the
  existing code's logic as well as domain knowledge — so no single agent can cover the whole process and they
  must be integrated.
- He lists what an IDE agent orchestration system should support: fast access to IDE context, lightweight
  context processing such as code search and static analysis, interaction with cloud agents through APIs,
  integration with third-party tools such as SonarQube, GitHub and Git, and encryption of sensitive information
  such as code and requirements.
- His Shire example defines a script that calls a remote agent deployed on Dify to fetch a business requirement,
  then, after the model analyses it, calls a local agent that generates SQL following the enterprise's SQL
  conventions.

## Context

The post is an argument for a direction rather than a report of results. The author connects it to his own
earlier work on the open-source IDE plugin [[SoftwareApplication/unit-mesh-auto-dev]], for which his team built
an AutoCRUD agent that took issues from GitHub or GitLab as requirements and modified code in the local
codebase.
