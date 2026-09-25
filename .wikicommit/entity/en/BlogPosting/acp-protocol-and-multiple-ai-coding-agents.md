---
title: "ACP 协议 + 多 AI 编程智能体：企业研发的新生产力平台"
type: "schema:BlogPosting"
lang: en
tags: [agent-protocols, coding-agents, multi-agent, governance, mcp]
sources:
  - type: url
    url: 'https://www.phodal.com/blog/agent-acp-in-practise/'
    hash: sha256:2b6ec051410853e3f6c810e69eecfcbeea93b7ae55d070290144a335cdcc9ca7
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A February 2026 Chinese-language blog post by Phodal Huang explaining the Agent Client Protocol, describing how his team integrated it into the AI coding tool AutoDev, surveying JetBrains' ACP ecosystem and multi-agent workspaces, and proposing a three-layer enterprise governance model of MCP/Skills, ACP and A2A."
  author: ["Phodal Huang"]
  datePublished: "2026-02-09"
---

This post, written in Chinese by Phodal Huang, starts from a problem he sees in enterprise development:
several AI coding assistants — the post names Cursor, Copilot, Augment and Claude Code — now tend to
appear in the same company, and platform teams must let them coexist across different editors without
giving up efficiency, collaboration or governance. His answer is the
[[DefinedTerm/agent-client-protocol]] (ACP), which his team had recently integrated into AutoDev, the AI coding
tool they build.

He says his interest in ACP began with wanting to offer customers a unified AI coding agent service on
an internal network. He contrasts enterprise work with vibe-coding demos: in an enterprise, people remain
responsible for their own code and AI is only an assisting tool, so AI-written code still needs a tool
for reviewing it. After finding that Claude Code's IDEA plugin did not work well for this, the team turned
to ACP as promoted by JetBrains.

## Key Points

- ACP is presented as a standard protocol between IDEs or editors and AI coding assistants, which the
  author suggests thinking of as "LSP for AI agents". Its core principle, as he puts it, is letting the
  IDE fully control every step the agent takes, by making tool calls first-class and visible to the IDE.
- The author describes its working model as the IDE acting as client and the agent as a server
  subprocess, communicating over JSON-RPC 2.0 on stdio, with capability negotiation at start-up,
  real-time updates on plans and tool calls during a session, and permission requests for sensitive
  operations such as editing files or running commands.
- AutoDev's integration, made while building AutoDev 3.0 (Xiuper) around a unified rendering
  architecture, was bidirectional — AutoDev can act as an ACP server and as an ACP client —
  using the official Kotlin and TypeScript SDKs, and was built around a common renderer interface so
  that ACP events are rendered on multiple platforms; agents that do not speak ACP, such as Claude Code,
  are adapted by parsing their own streaming output.
- JetBrains, which the author calls one of ACP's main promoters, offers an official ACP Agent Registry
  for one-click installation and runtime management, custom configuration through an `acp.json` file,
  and MCP integration for agents running under ACP.
- He summarises the relationship between the two protocols as ACP handling interaction between agent
  and IDE while [[DefinedTerm/model-context-protocol]] extends the agent's capabilities to external
  systems.
- He describes multi-agent workspaces that ACP makes easier to build: Augment Intent, which he had been
  invited to use, with a coordinator agent splitting tasks among specialist agents working in separate
  worktrees, and [[SoftwareApplication/google-antigravity]] with its editor view and agent manager
  surface.
- He proposes a three-layer governance model for enterprise AI platforms: MCP and Skills as the carrier
  of reusable enterprise capabilities, ACP as the interaction layer between developers and assistants,
  and [[DefinedTerm/agent2agent-protocol]] as the collaboration network among agents.

## Context

The post is a practitioner's account of his own team's integration work combined with a survey of
vendors' offerings; it reports no measurements. Its enterprise recommendations — that now is the best
time to build a multi-agent development platform — rest on the author's own view of where the ecosystem
is heading.
