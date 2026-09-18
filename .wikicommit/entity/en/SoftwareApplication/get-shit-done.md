---
title: "Get Shit Done (GSD)"
type: "schema:SoftwareApplication"
lang: en
aliases: ["GSD"]
tags: [agents, coding-tools, context-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A lightweight system of meta-prompting, context engineering and spec-driven development for use with Claude Code, operating as a layer of commands and conventions over the agent rather than as its own platform."
  applicationCategory: "Context-engineering and spec-driven development layer"
  featureList: "Meta-prompting; explicit context assembly deciding what the agent reads and in what order; conversion of broad requests into specifications and executable steps"
---

Get Shit Done (GSD) presents itself as a lightweight system of meta-prompting,
[[DefinedTerm/context-engineering]] and [[DefinedTerm/spec-driven-development]] for use with
[[SoftwareApplication/claude-code]]. Rather than defining its own platform, it operates as a layer of
commands and conventions over the agent, focused on structuring the context provided to the model and
on turning broad requests into specifications and executable steps. It is one of the six frameworks
assessed in [[ScholarlyArticle/from-prompt-to-process]].

## Capabilities

GSD's distinguishing move is to treat context assembly as an explicit engineering task: it decides what
the agent should read, in what order and under which framing, before acting. The assessing study
connects that emphasis to work on grounding hooks in the spec-driven development literature, which
reports that agents can go blind to context in large repositories.

## Adoption & Ecosystem

Under the [[DefinedTerm/six-dimension-process-taxonomy]], GSD scores 2 on context, 1 on specification
and 0 on roles, validation and portability, with 1 on execution — a total of 4 out of 12, the lowest of
the six frameworks assessed, and the only one to score zero on three dimensions. GSD is the framework
that study describes as most focused on context, and that study treats the six dimensions as
complementary reading lenses rather than disjoint partitions, so a single feature may score on more
than one of them. The scores express the study author's judgement from official documentation, assigned
by a single rater with no second independent coder, rather than an independent empirical measurement.

Two limitations are named. Because GSD is strongly coupled to a specific agent, its portability is more
limited than that of [[SoftwareApplication/github-spec-kit]] or [[SoftwareApplication/openspec]], and
its effectiveness depends on the
quality of the prompt conventions a team adopts. The study also notes that the repository signalled a
maintenance move to a new organisation, which it offers as an illustration of the volatility typical of
recent community frameworks — the same volatility it lists among the field's recurring risks, alongside
the supply-chain exposure that installable command kits and agent conventions carry.
