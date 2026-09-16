---
title: "Context Before Code: An Experience Report on Vibe Coding in Practice"
type: "schema:ScholarlyArticle"
lang: en
tags: [vibe-coding, ai-assisted-programming, software-engineering]
sources:
  - type: url
    url: https://arxiv.org/pdf/2603.11073
    hash: sha256:b27050eee67fa3ab8d502b496b64c26c1985857ac4dabac280117ba6882031d7
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An experience report from a small full-stack team on building two production-oriented AI systems (a multi-tenant agent learning platform and an academic RAG system) using contextual vibe coding under explicit architectural constraints, finding that generated code reliably handled scaffolding but not tenant isolation, access control, or asynchronous processing without deliberate manual design."
  author: ["Md Nasir Uddin Shuvo", "Md Aidul Islam", "Md Mahade Hasan", "Muhammad Waseem", "Pekka Abrahamsson"]
  datePublished: "2026-03-10"
  keywords: ["Vibe coding", "AI-assisted development", "RAG systems", "agent memory", "multi-tenancy", "experience report"]
---

This EASE 2026 experience report examines how conversational "vibe coding" behaves when building
two production-oriented AI systems under explicit architectural constraints: a multi-project agent
learning platform with structured memory and strict tenant isolation, and a file-aware academic
retrieval-augmented generation (RAG) system with citation tracing and role-based access control.
Both systems were developed by a small full-stack team at Tampere University, with requirements —
including tenant isolation, asynchronous execution, and controlled retrieval — defined before
implementation began, and validated afterward through structured manual testing, code inspection,
and runtime log analysis.

Across both systems, vibe coding accelerated scaffolding and feature implementation — API routes,
serialization utilities, and interface components — but the generated code consistently
under-specified architectural properties that were not explicitly stated in prompts: early routes
omitted project-level filtering in database queries (risking cross-project data access), and
memory-update and embedding routines initially executed synchronously despite an asynchronous
requirement, both of which required manual correction. The paper reports a resulting shift in
engineering effort away from boilerplate implementation and toward constraint specification,
isolation auditing, and enforcement validation, and identifies recurring architectural areas — which
it terms "non-delegation zones" — where conversational code generation remained insufficient for
production reliability.

## Key Points
- Reports that vibe coding reliably accelerated routine scaffolding (API routes, database models,
  UI components) in both systems, but rarely preserved architectural properties — tenant isolation,
  access control, and asynchronous processing — unless those constraints were made explicit in
  prompts
- Identifies a recurring shift in engineering effort: reduced effort on boilerplate writing, CRUD
  scaffolding, basic routing, and UI templates, and increased effort on architecture design,
  isolation auditing, policy specification, and validation/monitoring
- Proposes the concept of architectural "non-delegation zones" — recurring areas (multi-tenancy,
  access control, memory policies, asynchronous processing) that the authors found conversational
  code generation could not reliably handle without deliberate manual architectural design and
  verification
- Reports that infrastructure decisions such as background task queuing could not be safely
  deferred: early prototypes that ran inference and embedding synchronously became unstable under
  repeated use and had to be moved to background workers
- Argues, based on these two cases, that AI-assisted development is most effective as a tool for
  rapid implementation within clearly specified architectural boundaries rather than as a
  replacement for system-level design

## Notes
- This is a retrospective, two-case experience report by a small team with prior full-stack and
  infrastructure experience; the authors state the findings are experience-based insights rather
  than broadly generalizable conclusions, and note their own involvement in building both systems
  as a potential source of bias, which they sought to mitigate by grounding the analysis in
  observable artifacts (commit history, runtime logs, documented prompts) rather than recollection
- No controlled experiments or quantitative productivity/code-quality/defect-rate measurements were
  conducted
