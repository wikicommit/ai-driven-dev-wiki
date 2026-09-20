---
title: "OpenHands"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-agents, llm, software-engineering, open-source]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2407.16741'
    hash: sha256:01c47d5b7e938859b4b50218e91582dfc7f340a1b2c75d210d80be48372dc1f6
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An open platform for developing AI agents that interact with the world as a human developer does — writing code, working at a command line, and browsing the web — with sandboxed code execution, multi-agent coordination and built-in evaluation benchmarks. Formerly known as OpenDevin."
  applicationCategory: "AI agent development platform"
  featureList: "Implementation of new agents; safe interaction with sandboxed environments for code execution; coordination between multiple agents; incorporation of evaluation benchmarks"
---

OpenHands, formerly known as OpenDevin, is a platform for the development of powerful and flexible
AI agents that interact with the world in similar ways to those of a human developer: by writing
code, interacting with a command line, and browsing the web. It is introduced in
[[ScholarlyArticle/openhands-an-open-platform-for-ai-software-developers-as-generalist-agents]],
which presents it against the background of rapid development in AI agents that interact with and
affect change in their surrounding environments.

It is released under the permissive MIT license, and the introducing paper describes it as a
community project spanning academia and industry, with more than 2.1K contributions from over 188
contributors at the time of writing. Its code is stated to be at
<https://github.com/All-Hands-AI/OpenHands>.

## Capabilities

The introducing paper describes four things the platform allows for: the implementation of new
agents; safe interaction with sandboxed environments for code execution; coordination between
multiple agents; and the incorporation of evaluation benchmarks.

## Adoption & Ecosystem

Because evaluation benchmarks are incorporated into the platform itself, the benchmarks it holds are
part of what it offers. The introducing paper reports an evaluation of agents over 15 challenging
tasks based on the benchmarks currently incorporated, spanning software engineering — for which it
names [[Dataset/swe-bench]] — and web browsing, for which it names WebArena, among others.
