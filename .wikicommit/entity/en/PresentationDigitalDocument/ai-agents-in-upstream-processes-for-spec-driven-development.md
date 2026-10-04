---
title: "仕様駆動開発を実現する上流工程におけるAIエージェント活用"
type: "schema:PresentationDigitalDocument"
lang: en
tags: [requirements-engineering, specifications, coding-agents]
sources:
  - type: url
    url: 'https://speakerdeck.com/sergicalsix/shi-yang-qu-dong-kai-fa-woshi-xian-surushang-liu-gong-cheng-niokeruaiesientohuo-yong'
    hash: sha256:3d30a67880494fd65cb9ca2b42e32bf110913e5d68f9205c31ecae48960b4083
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "Japanese-language slide deck from the AI-Driven Development Conference 2025 Autumn arguing that spec-driven development should be extended upstream into requirements work, and showing how AI agents can be designed for that phase."
  author: ["sergicalsix"]
  datePublished: "2025-10-30"
  recordedAt: "AI-Driven Development Conference 2025 Autumn"
---

This deck was presented at the AI-Driven Development Conference 2025 Autumn by sergicalsix, a tech lead in AI transformation at Algomatic. Its description notes that, being talk material, some of it is high-context or less than rigorous. The deck argues that AI coding tools concentrate on the implementation phase of the development cycle, and that [[DefinedTerm/spec-driven-development]] can best address their remaining problems if its scope is widened from implementation to the upstream phases of requirements work.

## Details

- **AI coding and its problems.** The deck describes AI coding and [[DefinedTerm/vibe-coding]] as conveying the "vibe" or intuition of the desired application to an AI and generating code through dialogue, and notes that AI coding has focused mainly on the implementation step of a development cycle running from requirements definition through basic and detailed design to unit, integration and system testing. It names three remaining problems: limits on handling complex development, difficulty controlling output (unexpected behaviour, such as removing one feature while adding another), and a lack of knowledge management — the reasons behind a specification cannot be left in a document when requirements are settled only in conversation.
- **Comparing remedies.** As of October 2025, the deck rates [[DefinedTerm/context-engineering]], division of responsibility (for example sub-agents), test-driven development, spec-driven development and model improvement against the three problems, and singles out spec-driven development as the talk's subject. Its contrast with ordinary AI coding is that spec-driven development leaves the specification (design document) behind as an intermediate artefact that is written and revised, rather than going straight from conversation to source code. [[SoftwareApplication/kiro]] is shown as an example tool, noted for letting development proceed in spec-driven fashion from the concept stage, working from proposals and rough drafts, and adopting frameworks such as the EARS format.
- **The gap upstream.** The deck observes that existing AI-driven tools leave areas unaddressed in both the upstream and downstream phases: practical requirements definition is described as too large and difficult for existing mechanisms and tools to solve, and connecting to core systems and handling confidential data are difficult from a security and governance standpoint. Because the requirements and needs-definition phases feed directly into what is built, they have the greatest influence on the result; the deck distinguishes wishes (what one would like to do), needs (what should be done) and requirements (what will be done), and points to a gap between where AI-driven development tools act and where the development cycle is most sensitive. Its proposal is to widen spec-driven development's scope to these upstream phases.
- **Designing agents for upstream work.** Upstream work — putting wishes into words, building agreement among stakeholders, absorbing ambiguity and uncertainty, organising requirements without gaps, creating and updating documents, and drawing lines on scope and priority — requires handling a great deal of context. The deck lays out a flow in which events accumulate within a session and are persisted as memory such as specifications, and names three design concerns as key: the context, how memory accumulates, and the expected output. For context, it recommends diverse, high-quality and concrete material; for memory such as specifications, a granularity that people can interpret and AI can reproduce as a program.
- **What, why and why not.** The deck's worked example adds a filter to a hotel availability search: recording only the *what* leaves the reason unknown, while adding *why* (plans with only one or two rooms left often fill up between clicking "book" and confirmation) and *why not* (merely excluding zero-inventory plans had not reduced "fully booked" errors) makes the background, assumptions and specification explicit. Two agent patterns are proposed for filling in context: a question-asking agent that works from a list of questions asking why and why not, and an agent that reuses information from similar past projects to update a specification.
- **Speeding up communication.** Because much upstream work is communication and alignment, the deck shows a multi-agent arrangement in which sub-agents draft screen-transition diagrams and screen mock-ups in response to a proposed feature. Its conclusion is that AI agents should be designed flexibly according to each purpose.
