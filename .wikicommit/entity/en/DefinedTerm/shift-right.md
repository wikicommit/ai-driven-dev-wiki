---
title: "Shift Right"
type: "schema:DefinedTerm"
lang: en
aliases: ["Shift-Right"]
tags: [devops, production-feedback, software-quality]
sources:
  - type: url
    url: 'https://www.codecentric.de/wissens-hub/blog/shift-left-and-right-wie-ki-integration-ueber-das-coding-hinauswaechst'
    hash: sha256:c56eb7ca57b7c6a3d943d7e214b28e500b4b15141ffd4b5854443353c81b9ebc
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The practice of moving quality gates and test execution into the real runtime context after release — through feature flags, canary releases, telemetry and similar techniques — and learning systematically from production."
---

Shift Right is the practice of moving quality gates and test execution into the real runtime context, learning systematically from production what cannot be verified with certainty before release. [[BlogPosting/shift-left-and-right-how-ai-integration-grows-beyond-coding]] describes it as having emerged later than [[DefinedTerm/shift-left]], as its counterpart, and counts canary releases, feature flags, A/B tests and observability practices as Shift Right movements that share one principle: what cannot be checked with certainty before release is checked after release, in controlled steps, with real users.

## Usage

The codecentric post treats Shift Right as purely technical safeguarding — whether the deployment works, whether performance holds, and whether errors appear under real load — and distinguishes it from a product-level learning loop that checks whether the right problem is being solved for the user. When a Shift Right check fails, for example because a canary release aborts or error rates rise, the result flows back into the creation loop as a concrete bug or incident. In AI-assisted development it names the AI support available at this stage as auto-triage of incidents by severity and suspected cause, root cause analysis over logs and stack traces, anomaly detection of behavioural deviations before they become outages, and auto-remediation such as a rollback when performance drops.

## When It Applies

The post argues that Shift Right assumes structurally anchored learning loops: a regular forum in which production data is evaluated, and a rhythm in which incident trends turn into roadmap changes. Without them, it says, the result is "Shift-Right theatre" — the data exists but goes unused — and it names this as the most common reason AI initiatives fail at Shift Right, in the experience it reports. It reports that the AI tooling is technically available but used by few teams because no concrete pipeline steps have been built for it, and rates its maturity in Germany as just emerging — present in large organisations, but not scaling.

## Related Terms

- [[DefinedTerm/shift-left]]
- [[DefinedTerm/outer-loop]]
