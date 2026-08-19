---
title: "From spec to production: a three-week drug discovery agent using Kiro"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, agentic-coding]
sources:
  - type: url
    url: 'https://aws.amazon.com/blogs/industries/from-spec-to-production-a-three-week-drug-discovery-agent-using-kiro/'
    hash: sha256:88a7c9517554f4f93af74e1fddd0380527eccaa4427916af91e6ffd946845cff
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "AWS Industries blog post of 18 February 2026 reporting a production-ready target identification agent built by three developers in three weeks using Kiro's spec-driven workflow. Its methodological content — the three specification documents, steering documents and agent hooks — is what makes it relevant beyond its life sciences domain."
  author: ["Necibe Ahat", "Ariella Sasson", "Deepesh Koppunuru", "Hamza Mahmood", "Mingfei Bi", "Michael Steward"]
  datePublished: "2026-02-18"
  publisher: "AWS"
---

This post on the AWS Industries blog, dated 18 February 2026 and written by six authors, reports on a project rather than a product: an AWS team built a production-ready target identification agent for drug discovery "in just three weeks with three developers", and the post shares its methodology, architecture decisions and lessons. It is included in this wiki for the methodology — a concrete, dated account of [[DefinedTerm/spec-driven-development]] practised end to end with [[SoftwareApplication/kiro]] — rather than for the life sciences use case, which is outside this wiki's subject area.

The post's framing of why spec-driven development was chosen is an explicit contrast. It describes [[DefinedTerm/vibe-coding]] as "the iterative, exploratory approach where developers write code directly based on intuition and immediate needs, refining through trial and error", says that while this "can work for small prototypes, it becomes challenging to scale the solution and ensure the quality and consistency of the generated code", and sets against it spec-driven development, which "by contrast, separates planning from execution", with detailed specifications created before any code is written.

## Key Points

- **Three specification documents per feature**, created in order from an initial prompt, each reviewed before the next: `requirements.md` for what is being built, including feature requirements, acceptance criteria and success metrics — the "why" and "what" in terms stakeholders can validate; `design.md` for the technical architecture, implementation approach and integration points, documenting decisions about frameworks, APIs and data flows; and `tasks.md` breaking the design into actionable implementation steps, each "granular enough for autonomous execution while maintaining context about the broader feature".
- **Four stated advantages** of that structure: it creates the context that lets the tool implement features autonomously while developers review and validate; it makes onboarding trivial, since new team members can read the specs to learn what was built and why; it lets a team say "develop a new feature based on the previous implementation with the same tech stack"; and — the one the post calls most important — it keeps human-in-the-loop oversight *at the planning stage*, so a misunderstanding is corrected in the documents rather than in code, which the post says prevents costly rework.
- **Three steering documents** for project-wide consistency: a `product` document defining purpose and key capabilities, a `structure` document enforcing organizational principles such as tool abstraction patterns and error handling standards, and a `tech` document specifying the stack and development guidelines. The post distinguishes them from specifications by scope — steering documents cover the entire project, specifications a specific feature — and notes they are added automatically as context.
- **Agent hooks for routine work**: hooks listened for file system events and ran predefined prompts in the background, in this case keeping `README.md` documentation updated as code changed, with the post also naming test generation, performance optimization and coding-standard maintenance as delegated tasks. Because hooks are stored at repository level, the whole team got the automation on checkout.
- **A three-week breakdown**: days 1–3 requirements gathering and stakeholder alignment; days 4–6 technical design and architecture decisions; days 7–14 creating specs and implementing the full-stack web app; days 14–21 testing, feedback, and iteration on prompt engineering and feature requests.
- **Reported outcomes**, all the team's own figures: the tool "generated more than 95% of the business logic code, saving over 80 hours development time"; tool-written README documentation saved an estimated 8 hours; and all team members followed the same coding standards and frameworks through the steering documents.
- **Five takeaways**: invest in specifications upfront; start with comprehensive steering documents; connect to [[DefinedTerm/model-context-protocol]] knowledge sources to improve generation accuracy; trust your data and label everything else — nothing in a production system should be simulated, and any test data used during development must be explicitly marked in both the data and its outputs, because unlabelled test data that looks accurate becomes hard to distinguish from a real response; and build observability from day one.

## Context

The post's summary of what changed in how the work was done is the sentence most portable out of its domain: "the spec-driven approach in Kiro shifted our development from being about authoring each line of code to guiding and delegating tasks to the AI agent to complete with human oversight." Its account of team shape follows from that — three solution architects each working independently on their own tools and integrations, kept coherent by the shared specs, while the tool handled repetitive coding.

Every figure and benefit claim here is AWS's own, from a post published by the vendor of both the coding tool and the cloud services used; there is no independent evaluation, and the team was writing about a project it undertook partly to demonstrate that the approach works. The post also relays a second party's numbers — a customer it says completed 52 weeks of estimated work in three weeks with a 90% efficiency increase — which is reported at one remove and should be read as such.

The post closes on two future directions the team had not yet used in this project: **Kiro Powers**, described as specialized expertise modules that load context and tools on demand to solve what the post calls "the context overload problem of traditional MCP servers", bundling MCP tools, steering files and hooks with built-in best practices and activating only when relevant; and a **Kiro Autonomous Agent**, described as a frontier agent meant to handle software development work as an asynchronous teammate, able to learn from agents already built in the IDE and apply the same patterns to build more without constant human guidance.
