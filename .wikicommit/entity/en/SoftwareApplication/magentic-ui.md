---
title: "Magentic-UI"
type: "schema:SoftwareApplication"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2507.22358'
    hash: sha256:4c69a2b79f2218dce03ec5fce115f496675c20428e05321690b1ff4205bd0205
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An open-source, human-in-the-loop web interface from Microsoft Research for developing and studying human-agent interaction, built on an extensible multi-agent system that can browse the web, execute code, and manipulate files, and can be extended with Model Context Protocol (MCP) tools."
  applicationCategory: "Human-in-the-loop agentic system"
  author: "Microsoft Research AI Frontiers"
  featureList: "Co-planning; co-tasking; action approval; answer verification; long-term memory; multi-tasking"
---

Magentic-UI is an open-source, end-user-facing web interface, introduced in [[ScholarlyArticle/magentic-ui]] by Microsoft Research AI Frontiers, for developing and studying human-in-the-loop agentic systems. It is powered by an extensible multi-agent system adapted from Magentic-One that can browse and act on the web, generate and execute code, and generate and analyze files, and can be extended with Model Context Protocol (MCP) tools via custom agents that wrap one or more MCP servers. Its architecture consists of a lead Orchestrator agent, implemented using AutoGen, that directs a set of sub-agents — including WebSurfer, Coder, and FileSurfer — to perform actions, with the human user treated as a special-role agent within the multi-agent team.

## Capabilities

Magentic-UI offers six interaction mechanisms for low-cost human involvement: co-planning (collaborating on a plan of action before execution begins), co-tasking (seamlessly taking over or handing back control mid-task), action approval (requiring user sign-off on high-stakes actions), answer verification (helping the user validate that a task was completed correctly), memory (saving and reusing past task workflows to improve future performance), and multi-tasking (running multiple sessions in parallel while staying in the loop). The Orchestrator has two operating modes — a planning mode, where it collaborates with the user to produce a plan, and an execution mode — and it will ask the user a clarifying question when a task is ambiguous or under-specified before generating a plan.

For safety, Magentic-UI runs each of its agent components in a separate sandboxed Docker container, uses its own browser distinct from the user's so that credentials and session cookies are not shared, and supports an allowed-websites list: visiting any site outside that list requires explicit user approval, with Magentic-UI stating the exact URL, page title, and reason for the visit.

## Adoption & Ecosystem

Magentic-UI is open-source, hosted at github.com/microsoft/magentic-ui, and is built on the architecture of Microsoft's earlier Magentic-One multi-agent system. It is positioned as a research prototype meant to help researchers study open questions in human-in-the-loop oversight of AI agents, and its simulated-user evaluation methodology draws on prior work including τ-bench and Co-Gym.
