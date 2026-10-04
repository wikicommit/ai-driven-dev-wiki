---
title: "Spec-driven Development mit KI-Agenten – Wie Spezifikationen Code, Tests und KI-Agenten in Softwareprojekten synchron halten"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, harness-engineering, enterprise-software, traceability]
sources:
  - type: url
    url: 'https://ai-engineering-summit.de/blog/spec-driven-development-ki-agenten/'
    hash: sha256:53083788f1424de4a3df3ee2f9dc8a768c1b897e3ceb3c6dba73e3f29f05fc19
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A German-language article by Simon Martinelli on the AI Engineering Summit blog that presents spec-driven development through his AI Unified Process, walking through a use case, an entity model and a traceable test for the Spring PetClinic, and arguing that the approach suits long-lived enterprise systems."
  author: ["Simon Martinelli"]
  datePublished: "2026-07-21"
  publisher: "AI Engineering Summit"
---

This article argues that AI agents writing code in minutes does not solve the core problem of software
development: whether people still understand what behaviour a system is supposed to have. When
requirements, architecture decisions and tests drift away from generated code, the code becomes the only
reference. [[DefinedTerm/spec-driven-development]] is presented as the answer, with the specification as the
starting point from which code and tests are derived and with which they must stay in sync.

The author describes arriving at this from his own experience: after building a volunteer-management
application with vibe coding, he lost track of what was implemented and why, because much of that knowledge
lived only in chat history. He recalled using use cases on projects at SBB in the early 2000s, tried them as
the structure for his specifications, and describes this as the beginning of the
[[DefinedTerm/ai-unified-process]] (AIUP), after which he threw the existing code away and started again. Most
of the article explains AIUP's three layers and demonstrates them on the Spring PetClinic, the Spring
Framework's official sample project.

## Key Points

- The article distinguishes AIUP from tool-led spec-driven workflows such as Amazon Kiro, GitHub Spec Kit and
  the BMad method, saying that in long-lived business applications requirements must be discussed and
  maintained with domain experts, product owners, architects and testers, not only within the development
  team.
- AIUP separates three layers: the "what" (use cases and an entity model, together forming the
  specification), the "how" (the implementation) and the "with what" (guardrails between them, also called
  the harness).
- A use case typically contains an identifier, a title, actors, preconditions, a numbered main flow,
  alternative flows, postconditions and business rules, written in the language of the domain rather than of
  the code; the author considers user stories usually too vague as direct input for AI code generation.
- The "with what" layer consists of [[DefinedTerm/agent-skills]] holding reusable project knowledge,
  [[DefinedTerm/model-context-protocol]] servers giving the AI current documentation and examples, and
  guidelines recording rules such as naming conventions, package structure and architecture decisions.
- The author links this layer to Birgitta Böckeler's application of harness engineering to coding agents and
  her distinction between guides that steer the model beforehand and sensors that give feedback afterwards
  (see [[DefinedTerm/guides-and-sensors]]).
- Tests are derived from use cases; each test method carries a custom `@UseCase` annotation naming the use
  case ID, scenario and business rules it covers, so traceability from specification to implementation
  arises as a side effect and affected tests are easier to find when the specification changes.
- The author argues that the "this sounds like waterfall" objection misreads the approach, which works
  iteratively use case by use case rather than writing every specification up front.
- [[DefinedTerm/domain-driven-design]] bounded contexts are proposed as the structuring principle: each
  context has its own use cases, entity model and code, which keeps the AI's context small and reduces
  confusion between terms.
- From his own experience, the author finds that AIUP works best with small teams — two developers per
  bounded context as a starting point, not a rule — working trunk-based, and that Kanban often fits better
  than Scrum because use cases vary in size.
- For existing systems, an AI agent reconstructs use cases and the entity model from existing code and tests,
  and a requirements engineer reviews them with the business side before modernisation.
- He names three recurring pitfalls: use cases turning into technical scripts that describe the UI,
  specification, code and tests drifting apart (countered by discipline and an automated drift check), and
  starting with tooling before the method.

## Context

The article is one practitioner's account of a method he developed himself, published on the blog of a
training conference whose programme covers agentic software engineering. Its recommendations on team size,
process and workflow rest on the author's own project experience rather than on measurements. It mentions the
AIUP Marketplace plug-ins for Claude Code and other agents as one possible toolset, while stating that they
are not a prerequisite for the method, and it closes by arguing that the gain from spec-driven development is
not faster code generation but keeping business intent visible, which it considers decisive for long-lived
business applications.
