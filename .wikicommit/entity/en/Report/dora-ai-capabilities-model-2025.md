---
title: "DORA AI Capabilities Model"
type: "schema:Report"
lang: en
tags: [dora, ai-adoption, developer-productivity, empirical-study]
sources:
  - type: url
    url: 'https://services.google.com/fh/files/misc/2025_dora_ai_capabilities_model.pdf'
    hash: sha256:f65a8b062d822c14999309f1737296bccd7ef75c13fbe6d3f4066a1443085a23
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Google's DORA report (v. 2025.1) presenting the DORA AI Capabilities Model — seven technical and cultural capabilities its 2025 research found to amplify the positive impact of AI adoption — with guidance on implementing, measuring and prioritizing them."
  publisher: "[[Organization/google]]"
  abstract: "Based on survey responses from nearly 5,000 technology professionals and over 100 hours of qualitative data, the report argues that AI's primary role in software development is to amplify an organization's existing strengths and dysfunctions, and details seven capabilities that amplify AI's positive effects, together with team profiles, value stream mapping and a prioritization workshop for acting on them."
---

The DORA AI Capabilities Model report, version 2025.1, is published by Google's DORA research programme
as a practical companion to its 2025 State of AI-assisted Software Development report, which first
introduced the model. It presents the [[DefinedTerm/dora-ai-capabilities-model]]: seven capabilities,
spanning technical and cultural domains, that DORA's 2025 research found to amplify the positive impact
of AI adoption on outcomes such as individual effectiveness, team and product performance, code quality,
throughput and organizational performance. The report describes the model as complementary to the
long-standing DORA Core Model, not a replacement for it.

The findings draw on research DORA conducted in 2025 comprising more than 100 hours of qualitative data
and survey responses from nearly 5,000 technology professionals. For each capability the report explains
why it matters for AI, how to improve it, common obstacles, and how to measure it — listing the DORA
survey questions used and additional metrics. It closes with tools for acting on the model: team
profiles from a cluster analysis, value stream mapping, and a 90-minute team prioritization workshop.
The report is licensed under CC BY-NC-SA 4.0.

## Findings

- The report's central claim is that AI is an amplifier: it magnifies the strengths of high-performing
  organizations and the dysfunctions of struggling ones, so the greatest returns come from investing in
  foundational systems rather than from the tools themselves.
- 90% of survey respondents use AI as part of their work.
- Each capability amplifies AI's effect on particular outcomes: a clear and communicated AI stance on
  individual effectiveness, organizational performance and throughput, while also reducing friction;
  healthy data ecosystems on organizational performance; AI-accessible internal data on individual
  effectiveness and code quality; strong version control practices on individual effectiveness
  (through commit frequency) and team performance (through reliance on rollback); working in small
  batches on product performance, while also reducing friction; user-centric focus on team
  performance; and quality internal platforms on organizational performance.
- Working in small batches slightly reduces the individual-effectiveness gains teams perceive from AI.
  The report offers three hypotheses (the overhead of decomposing work, the friction of reviewing small
  chunks of machine-generated code, and tools better suited to large changes) and argues the product and
  friction benefits outweigh this.
- Adopting AI-assisted development tools can harm teams that lack a user-centric focus: with low
  user-centricity, AI adoption is associated with decreased team performance.
- When internal platform quality is low, AI adoption's effect on organizational performance is
  negligible; when it is high, the effect becomes strong and positive. 90% of organizations have adopted
  internal platforms and 76% have dedicated platform teams.
- About 21% of respondents are beginning to store AI prompts in version control.
- AI adoption alone has only a modest impact on organizational performance, and that effect is amplified
  when paired with strong value stream mapping practices.
- A cluster analysis of eight outcome factors yields seven team archetypes, from "foundational
  challenges" (10% of respondents) and "the legacy bottleneck" (11%) to "pragmatic performers" and
  "harmonious high-achievers" (20% each); the report notes the names and descriptions are an
  interpretation of the data.

## Guidance

For a clear AI stance, the report recommends a cross-functional working group producing a risk-based
policy that sorts uses into three buckets — prohibited, permitted with guardrails (for example
human-in-the-loop review of all AI-generated code), and allowed — published as a living document. For
AI-accessible internal data it contrasts prompt engineering with
[[DefinedTerm/context-engineering]], which it describes as the system that automatically gathers relevant
company data, up-to-date documentation, and tools and rules for the model, and it names retrieval-augmented
generation and a [[DefinedTerm/model-context-protocol]] server as the two emerging patterns for supplying
only the most relevant context. Under version control it recommends versioning everything, trunk-based
development, small frequent commits, and storing AI prompts and agent configuration files such as
GEMINI.md or [[DefinedTerm/claude-md]]. Under user-centric focus it points to
[[DefinedTerm/spec-driven-development]] as an emerging paradigm that orients LLMs toward user needs.
