---
title: "Frequent Intentional Compaction"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, compaction, agentic-coding, terminology]
sources:
  - type: url
    url: 'https://nyosegawa.com/en/posts/coding-agent-workflow-2026/'
    hash: sha256:bb7d36388cc5d0dc91fc90185585f6fff68833b1b198e732c6e2d6d41a285f45
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Compacting an agent's context preventively at each phase boundary to hold utilisation in a 40-60% band, rather than compacting reactively once the window is 80-100% full."
  termCode: "FIC"
  inDefinedTermSet: ""
---

Frequent Intentional Compaction — abbreviated FIC — is the practice of running [[DefinedTerm/compaction]] deliberately and often, at each phase boundary of a workflow, instead of waiting until the context window is nearly full. [[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] describes it as a distinguishing feature of the [[DefinedTerm/research-plan-implement]] workflow and attributes it to HumanLayer.

## Usage

Its stated operating target is to keep context utilisation between 40% and 60%. The contrast the technique is defined against is panic-compacting at 80-100% fill: compaction happens preventively and often rather than as an emergency response once quality has already degraded.

The reported result that survey relays is that on a 300k-line Rust codebase the approach let a team complete a week's worth of work in a single day. That figure comes from HumanLayer's own account rather than from independent measurement.

Because each phase boundary of a Research → Plan → Implement cycle already produces a durable artefact — `research.md`, `plan.md`, a progress file — compaction at those points is comparatively safe: what would otherwise be lost from the window has already been written to disk, which is the same "filesystem as persistent storage" principle the survey identifies across all long-session patterns.

## Related Terms

FIC is a scheduling discipline for [[DefinedTerm/compaction]] rather than a different mechanism, and it is one of the two answers to [[DefinedTerm/context-rot]] the survey presents — the other being keeping sessions short and starting fresh at each phase boundary. Its reliance on per-phase artefacts connects it to [[DefinedTerm/agentic-memory]], and the compaction risk it manages is the same one [[DefinedTerm/governance-decay]] documents at the safety-constraint level.
