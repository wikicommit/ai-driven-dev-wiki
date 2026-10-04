---
title: "バイブコーディングはもう古い！エージェンティックエンジニアリングで差をつけろ"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, agentic-engineering, code-review]
sources:
  - type: url
    url: 'https://zenn.dev/yamitake/articles/agentic-engineering-surpass-vibe-coding'
    hash: sha256:4c9ca54cba960a10ce98bb1494b6808a1b5a0f30f3d2049f8697244e30bca183
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An opinion piece arguing that by 2026 vibe coding has become commonplace but cannot carry production software, and proposing agentic engineering — orchestrating multiple AI agents while a human keeps final responsibility for architecture and quality — with five principles for practising it."
  author: ["JJ yamitake"]
  datePublished: "2026-02-24"
---

This post starts from [[DefinedTerm/vibe-coding]], recounting the term's coinage in February 2025 as
a style of coding that surrenders to the "vibes" and forgets the code exists, and asserts that by 2026
it has become ordinary — to the point that services have appeared through which non-engineers publish more than thirty web tools built this way and the
value of simply being able to write code is falling. Its question is what professional engineers
should do instead, and its answer is [[DefinedTerm/agentic-engineering]].

The author defines agentic engineering as a style of development in which a person directs and
coordinates multiple AI agents while retaining final responsibility for architecture and quality —
in the post's phrase, becoming the tech lead of an AI team rather than handing everything to the AI.
The post contrasts the two approaches, illustrates a division of work into implementation, testing
and refactoring agents under a human lead, and sets out five principles.

## Key Points

- The post identifies three limits of vibe coding: prototypes that run but are not fit for production
  (missing error handling, security holes such as SQL injection and XSS, performance problems,
  unmaintainable code); generated code that is a black box nobody can later fix, so technical debt
  accumulates until a rewrite looks cheaper; and an inability to handle complex requirements such as
  integrating several systems, legacy code, bespoke business logic and scalability.
- Its comparison table casts the human in vibe coding as a requester and in agentic engineering as
  designer and supervisor; one-to-one dialogue versus orchestration of multiple agents; quality left to
  the AI versus human review and approval; prototypes versus production products; and prompting skill
  versus design, prompting and review skill together.
- The author names [[SoftwareApplication/claude-code]] as the most practical environment for this
  style as of February 2026.
- Principle 1: decompose work into appropriately small tasks, so that each step's output can be checked
  and corrected, which the post calls the key to quality.
- Principle 2: pass context explicitly, structuring project background, constraints and conventions in
  files such as [[DefinedTerm/claude-md]] or a README.
- Principle 3: review is the human's job; AI-generated code must not be merged as-is, with a checklist
  covering security holes, N+1 queries, edge cases, consistency with existing code and test sufficiency.
- Principle 4: design on the assumption that agents fail — feature branches, automated tests in CI,
  preview environments and staged rollouts — to detect failures early and limit their impact.
- Principle 5: keep developing one's own expertise, since judging AI output depends on knowledge of
  architecture, security, performance and the domain; the post argues paradoxically that the better one
  uses AI, the more human expertise matters.
- The author concludes that an engineer's value is moving from writing code quickly and correctly to
  guaranteeing the correctness of code an AI has written, and frames this as an evolution, comparing it
  to doctors using surgical robots and pilots using autopilot.

## Context

The post is a short, polemical argument by an individual developer rather than a study, and its
definition of agentic engineering is presented as the author's own formulation. It closes with a
short list of reference links.
