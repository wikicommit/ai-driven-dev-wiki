---
title: "Программирование для тех, кто не пишет код: как устроен VibeCraft"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, multi-agent-systems, non-programmers]
sources:
  - type: url
    url: 'https://habr.com/ru/companies/yandex_cloud_and_infra/articles/1084654/'
    hash: sha256:3a39bfbcaf9b1ab426e9dd699c371ca1c03d2891de020bf64c99fa2f2c088392
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A post from Yandex's SourceCraft team explaining why it built VibeCraft, a chat-driven platform that lets non-programmers create and deploy applications, and how its two-agent design and managed deployment stack address the limits of vibe coding with general-purpose coding assistants."
  author: ["Robert Aksenov"]
  publisher: "[[Organization/yandex]]"
---

Published on Habr's Yandex Cloud & Yandex Infrastructure company blog, this post introduces [[SoftwareApplication/vibecraft]]. Its author, from the team behind the SourceCraft developer tools, opens with the downside of [[DefinedTerm/vibe-coding]] as practised with general coding agents: they confidently spend hours writing and testing code and then propose deploying a two-page pet project to a Kubernetes cluster with observability.

The argument is that current coding assistants assume a qualified developer who understands the project, can check the result and can phrase the next step, and that writing code is only part of shipping a product — someone must also rent a server, configure the environment, database and domains, and keep it running. A person without a technical background may not know those tasks exist, so working with an assistant becomes, in the post's image, like talking to a genie: the wish has to be stated precisely and with many non-obvious conditions, or the result matches the request and is useless in practice. VibeCraft is presented as the team's answer: the user attends to the product while the platform handles deployment.

## Key Points

- The team concluded at the start of 2026 that the technology had reached the point where people outside programming — marketers, accountants, analysts — could build their own products, which is the stated origin of VibeCraft.
- VibeCraft is contrasted with how programmers use agents such as Claude or Codex: first working out architecture, a detailed plan, a specification and testing rules, then letting several agents iterate for a long time. The post describes that approach as designed for experienced developers, and VibeCraft's as a short loop from idea to working prototype, refined iteratively.
- Inside is a two-agent system: a manager agent talks to the user, splits the request, asks clarifying questions and presents an editable plan; a programmer agent writes the code, sets up the environment, runs it and checks that it works.
- The post explains agent behaviour through a narrative account of language models: they continue the most plausible narrative in their data, so they will keep combining tools to attempt something they cannot do rather than admit the limit, and they follow the most salient scenario rather than the literal instruction. The team's stated goal is therefore to build the context so the desired narrative is already present in it.
- Its concrete example is the manager agent: given the ability to read files so it could keep track of a large backlog, it also wanted to edit them, and a prompt telling it it was a manager could not stop it, because the pretrained "I am a programmer" narrative outweighs the instruction. The fix was to give it a "write file" skill that always returns an error telling it that it is a manager and should assign the task to the developer.
- Recovery mechanisms include recreating the chat, so that a fresh agent reconstructs the state of the work, and a loop detector that cuts off incoherent output and restarts generation.
- Generated applications are Node.js full-stack TypeScript, chosen because a popular stack is better represented in model training data, with serverless YDB for storage so that no database servers need to be run.
- The post reports a simple prototype in 7–10 minutes, a task-list service in 20–30 minutes, and about 40 minutes from first message to a working task tracker.

## Context

This is a vendor's description of its own product, and its timings and design rationale are the team's own account; the author describes the field as new, with no time-tested recipes yet, and invites feedback.
