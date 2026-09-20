---
title: "ChatDev"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, multi-agent, coding-tools]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
  - type: url
    url: 'https://arxiv.org/abs/2307.07924'
    hash: sha256:615fc0d29f3cae50a8e97ac2aa2dccab1618f77299237bb910cf7c5129295e57
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A multi-agent system that simulates an end-to-end software company, with agents taking on roles such as CEO, CTO, and programmer to collaboratively design, implement, and test applications."
  applicationCategory: "Multi-agent coding system"
---

ChatDev simulates an end-to-end software company using a team of specialized AI agents. Agents take
on roles such as CEO, CTO, and programmer, and work together to design, implement, and test software
applications.

The paper that introduces it, [[ScholarlyArticle/chatdev-communicative-agents-for-software-development]],
describes ChatDev as a chat-powered software development framework whose specialized agents are
driven by large language models. Its motivation there is that applying deep learning to individual
phases of a waterfall model gives each phase its own uniquely designed model, which the authors
argue produces technical inconsistencies across phases. ChatDev's code and data are stated to be
available at <https://github.com/OpenBMB/ChatDev>.

## Capabilities

Agents in ChatDev are guided along two axes that the introducing paper names separately: *what* to
communicate, via a mechanism it calls a chat chain, and *how* to communicate, via one it calls
communicative dehallucination. The agents contribute to the design, coding and testing phases
through unified language-based communication, and solutions are derived from their multi-turn
dialogues rather than produced by a separate model per phase.

The same paper reports that the agents' use of natural language is advantageous for system design,
while communicating in programming language proves helpful in debugging — the two media are
presented as suiting different parts of the work rather than one replacing the other.

## Adoption & Ecosystem

A survey on AI agentic programming classifies ChatDev, in its comparative taxonomy, as a
"Multi-agent System" that is proactive and multi-turn with tool use, but not adaptive.
