---
title: "AI-Nativeという選択 ー 正解のない時代に、メルカリが選んだ指針"
type: "schema:BlogPosting"
lang: en
tags: [ai-adoption, context-engineering, spec-driven, software-process]
sources:
  - type: url
    url: 'https://engineering.mercari.com/blog/entry/20251225-mercari-ai-native-company/'
    hash: sha256:ed22a2b68e6e9e11d985d3ca79f7337bec6642349f4634d9b3bf2e9810a83cae
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Mercari's CTO sets out the company's guiding principles for becoming an AI-Native Company: redesigning work from an AI-first premise, treating knowledge management as its precondition, standardising development on Agent-Spec Driven Development, and inventorying every workflow in the company through an AI Task Force."
  author: ["kimurashunya"]
  datePublished: "2025-12-25"
  publisher: "[[Organization/mercari]]"
---

This post, whose title translates roughly as "Choosing AI-Native: the guiding principles Mercari chose in an age without right answers", is the written version of a keynote that [[Organization/mercari]]'s CTO gave at the company's mercari GEARS 2025 engineering event. It sets out how the company intends to become what it calls an AI-Native Company — a goal it quotes from its president as rebuilding products, ways of working and the organisation around AI — across the whole company rather than only in engineering. The author presents the principles as provisional: productivity gains from AI are described as still highly uncertain, and the post expects its own content to need updating as new technology appears.

Its argument has three parts. The company's precondition for AI-Native work is knowledge management, because agents need context — prominently including the history of decisions — that is currently scattered across tools. In development, the vehicle is [[DefinedTerm/agent-spec-driven-development]] (ASDD). Beyond development, an AI Task Force is converting the rest of the company's workflows, on the reasoning that faster coding alone cannot speed up releases if legal, security and compliance checks still wait on people.

## Key Points

- The post reports that 95% of Mercari's employees use AI tools, that AI accounts for about 70% of code generation, and that development speed rose 64% year on year — and states that the company nonetheless does not consider itself AI-Native yet, because coding productivity alone does not raise the productivity of the whole organisation.
- Its central reframing is from designing work around human limits to designing it around AI. Norms such as eight-hour days, eight-person teams and weekly meetings are described as optimised for human time, attention and capacity; the post suggests, as possibilities rather than findings, that smaller teams might achieve more if one person can cover several roles, and that shorter, high-focus working hours might be more productive if AI removes routine work. New work should instead be designed backwards from the value to be delivered.
- It attributes the company's initially disappointing productivity gains from AI coding assistants to a missing precondition: context. For coding it lists microservice dependencies, coding conventions, design documents, past decision logs for related work and code-review discussions as especially useful context, and names decision information — a project's aims, what is and is not acceptable, and what past discussions prioritised — as one of the most important kinds of context, and one that is often poorly organised, with discussions scattered across Slack, GitHub and meeting notes.
- To make information what it calls "AI-Readable", the company is consolidating it in Notion as a central knowledge base and redesigning how information is recorded, including standardising AI-generated meeting minutes.
- Before ASDD, the post reports, AI coding assistant use was widespread but uneven: prompt quality varied from person to person, gathering the right context was hard, generated code quality varied, and engineers used different tools — Cursor was rolled out company-wide at first, and newer assistants such as [[SoftwareApplication/claude-code]] then appeared — which made best practices hard to consolidate. It traces all four to the absence of a shared regulation for how to use AI.
- ASDD is presented as the development pillar, pursued in the Double project, whose name comes from its aim of doubling productivity. The post describes it as an AI-friendly, implementation-oriented specification template defining API definitions, data models, database schema, processing flow, test scenarios, concrete implementation steps and inter-service dependencies, so that anyone using an agent implements to the same quality and conventions. It stresses that ASDD's quality depends heavily on the quality of the context supplied when writing the Agent Spec. It also quotes a Mercari write-up of the project describing how one agent drafts the implementation plan from primary information while another checks it against coding conventions and security criteria, the two alternating until remaining uncertainties are put to the developer.
- The same Agent Spec is described as the base for agents across development (backend, frontend and mobile) and beyond it — QA test-case generation, AI review, customer-support specification research, risk management and compliance checks — and as the specification for PJ Aurora, a UI-generating agent that uses the company's in-house design system, alongside an agent that checks generated UI against the design rules.
- The AI Task Force started in July 2025, divided the company into 33 domains with one or two engineers and one or two project managers assigned to each plus a domain owner, and grew to about 100 members; the engineers were deliberately drawn from many fields rather than only from AI. By the time of writing it had inventoried the work in all 33 domains — about 4,000 workflows — and drawn up roadmaps, and was entering development of agents for them.
- The Task Force's reported lessons are that engineers working inside corporate functions such as legal and finance found redundant work and, in some cases, showed the possibility that the work itself could be made unnecessary; that setting priorities under high uncertainty was hard and slow in some domains; and that running 33 domains independently made decisions fast but left best practices and retrospectives poorly shared between them.

## Context

The post is a statement of direction from the company's own technology leadership, and its figures are the company's own. It frames AI-Native as an extension of the company's customer-centric values — freeing people to spend more time on the value delivered to customers — and connects it to the company's international expansion, arguing that agents could let it serve new markets with a realistic headcount.

It names security, governance and compliance around AI as themes it expects to grow in importance in the following year, while leaving them largely unaddressed here.
