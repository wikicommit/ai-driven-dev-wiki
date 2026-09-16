---
title: "Non-Delegation Zone"
type: "schema:DefinedTerm"
lang: en
tags: [vibe-coding, software-architecture]
sources:
  - type: url
    url: https://arxiv.org/pdf/2603.11073
    hash: sha256:b27050eee67fa3ab8d502b496b64c26c1985857ac4dabac280117ba6882031d7
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A recurring architectural area — such as multi-tenant data isolation, access control, memory-update policy, or asynchronous processing — where conversational code generation reliably fails to preserve required properties unless a human explicitly designs and verifies the constraint."
---

A non-delegation zone is a recurring architectural area in a software system where conversational
[[DefinedTerm/vibe-coding]] does not reliably produce correct results, and where a human must
instead perform deliberate architectural design and verification. The term was proposed in
[[ScholarlyArticle/context-before-code]], an experience report on building two production-oriented
AI systems, based on observing that generated code consistently omitted or under-implemented
certain system properties unless those properties were made explicit in prompts.

## Usage
In the two systems examined by that report, recurring non-delegation zones included multi-tenant
data isolation (generated database queries omitted project-level filtering unless explicitly
constrained), role-based access control, memory-update policies (what conversational input should
become persistent knowledge, and under what review process), and asynchronous processing
boundaries (generated code defaulted to synchronous execution of long-running tasks such as
embedding generation, which caused instability and blocking under load). The report contrasts these
zones with routine scaffolding — API routes, database models, serialization utilities, and
interface components — which conversational code generation handled reliably without requiring the
same level of manual correction.

The concept applies specifically to production-oriented systems where architectural properties
depend on domain-specific policy decisions rather than on functional behavior visible in a single
interaction. The report that proposed the term is based on a single two-case experience study by a
small team with prior infrastructure expertise, and its authors describe the findings as
experience-based insights rather than broadly generalizable conclusions.

## Related Terms
- [[DefinedTerm/vibe-coding]] — the development practice within which non-delegation zones were
  observed
- [[ScholarlyArticle/context-before-code]] — source of this concept and its supporting case studies
