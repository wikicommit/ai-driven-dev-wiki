---
title: "spec-code drift"
type: "schema:DefinedTerm"
lang: en
tags: [spec-driven-development, code-quality, verification, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.27045'
    hash: sha256:9004fd8330acfa64f27d8cc588f1234dd91b29303e4ee479b537bbdebca481f6
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The divergence that accumulates when code changes and its specification does not, leaving a system that still passes its tests while future agent runs are guided by a specification that no longer describes it."
  termCode: ""
  inDefinedTermSet: ""
---

Spec-code drift is the divergence between what a specification claims and what the code does, which accumulates whenever a specification is maintained as a separate document and developers update the code while deferring the spec update. [[ScholarlyArticle/the-spec-growth-engine]] treats it as one of two structural failure modes of AI-assisted development, and characterises its defining property as invisibility: a linter does not flag it, CI does not flag it, and the system ships with the drift baked in. The specification becomes "a historical artefact rather than a living contract, and future agent runs are guided by a lie."

The paper is explicit that the observation is old — it cites Reflexion Model work identifying the same pattern, and the coinage of "architectural erosion" in the same era — and locates what is new in the rate. When an AI coding agent generates several hundred lines per minute guided by a stale specification, the damage from a diverged spec accumulates far faster than in traditional development.

## Usage

That paper's proposed countermeasure is a **drift gate** built on two derived graphs. An *Intent Graph* is derived from the specification files, carrying contracts, invariants and acceptance criteria; an *Evidence Graph* is derived from static code analysis, carrying imports and exports, routes and events, and tests. A commit where the two disagree is blocked.

Four conditions are named as hard errors that block a merge unconditionally: orphan code, meaning a source file with no spec owner; an undeclared dependency, where code imports across a spec boundary with no declared edge; a dependency bypassing a contract, where code imports the internal files of another node; and a missing dependency contract, where a target node has no contract at all.

Three further conditions are reported as warnings without blocking: a declared dependency with no code evidence, a public export not mentioned in the contract, and contract behaviour with no test evidence.

The mechanism that makes the gate practical is coupling rather than diligence. The AI agent updates the affected specification in the *same commit* as the code change, the engine checks that delta against the evidence, and the human reviews only contract-level lines. The paper's stated claim for this arrangement is that it "transforms drift from a social/process problem into a structural impossibility" — keeping spec and code in sync is not left to discipline.

## Related Terms

Spec-code drift is the failure mode that [[DefinedTerm/spec-driven-development]] is most exposed to once the specification stops being enforced, and the same risk [[ScholarlyArticle/from-prompt-to-process]] records as the dominant one for [[SoftwareApplication/spec-kit]]: drift between artifacts and implementation where validation is weak. Its counterpart mechanism in the same framework is the [[DefinedTerm/spine]], which bounds what an agent reads rather than what it leaves behind.
