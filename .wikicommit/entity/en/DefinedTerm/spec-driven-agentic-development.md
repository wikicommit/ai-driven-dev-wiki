---
title: "Spec-Driven Agentic Development"
type: "schema:DefinedTerm"
lang: en
aliases: ["SDAD"]
tags: [spec-driven, sdlc, agentic-engineering, methodology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.20341'
    hash: sha256:60fe7cfcb300694e7d65079e069c14a90c5b43e1a04fb54734446018ec83d969
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A software delivery methodology proposed in a 2026 technical report, in which humans capture intent and formalise it as a machine-readable specification, coding agents synthesise the implementation from it, and independent verification plus human sign-off gate release."
---

Spec-Driven Agentic Development (SDAD) is the name
[[ScholarlyArticle/sdad-spec-driven-agentic-development-for-the-ai-native-sdlc]] gives to a
software delivery methodology that combines disciplined up-front formalisation with high-velocity
agentic implementation. Its authors argue that once coding agents can ingest entire repositories
and requirement documents, the binding constraint on delivery becomes the clarity of intent rather
than the speed of writing code, and that practice therefore converges toward the formal,
pre-emptive specification associated with Waterfall — which they present as a maturation of
practice rather than a regression.

## Usage

The report defines SDAD as four phases. Intent capture uses structured human–agent dialogue to
record requirements, constraints and business rules; formal specification turns that record into a
machine-interpretable blueprint of interfaces, logic, data structures and acceptance criteria;
agentic synthesis treats the specification as the authoritative input for multi-file generation of
code and tests; and independent verification checks the output against the specification through
automated test, security and conformance gates. Merge or release authority remains with an
accountable human, whom the report calls the Spec Architect, rather than with the synthesis agents.

Around this workflow the report proposes an SDAD-V model patterned on the classical V-model; a
redistribution of roles across engineering, QA, platform and product functions; metrics meant to
replace story points, including Spec Fidelity, the Ambiguity Tax and a Synthesis Efficiency Ratio;
hybrid estimation; and a gated migration path from Waterfall or Scrum. It frames SDAD as a mixed
regime with human accountability, not a human-absent pipeline.

## When It Applies

The report presents SDAD as applying where frontier agents with large context windows and
multi-agent orchestration are available to synthesise cross-module features from a specification,
and where a team can produce specifications precise enough to drive them; it assumes that
specification quality, verification gates and provenance logging are made first-class. It names
its own failure modes: a vague or malicious specification propagated across many files or services
in a single synthesis pass, human comprehension of agent-authored code falling behind, and
dependence on closed model vendors. Its standing is that of a single proposal: the report is
largely positional, labels its cost figures as illustrative rather than audited, and lists the
operational definition and measurement of its own metrics among its open questions.

## Related Terms

- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/agentic-engineering]]
- [[DefinedTerm/ai-native-software-engineering]]
