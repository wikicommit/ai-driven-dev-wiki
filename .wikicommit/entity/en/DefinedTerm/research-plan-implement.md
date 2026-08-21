---
title: "Research → Plan → Implement"
type: "schema:DefinedTerm"
lang: en
tags: [workflow, context-engineering, agentic-coding, terminology]
sources:
  - type: url
    url: 'https://nyosegawa.com/en/posts/coding-agent-workflow-2026/'
    hash: sha256:bb7d36388cc5d0dc91fc90185585f6fff68833b1b198e732c6e2d6d41a285f45
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A three-phase coding-agent workflow — deep codebase research, an annotated written plan, then batch implementation — whose core rule is that the agent writes no code until a human has reviewed and approved the plan."
  termCode: "RPI"
  inDefinedTermSet: ""
---

Research → Plan → Implement — abbreviated RPI — is a three-phase workflow for working with coding agents, described in [[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] as systematised by Boris Tane, a Cloudflare engineering lead, from nine months of Claude Code use, and as converging with methodologies developed independently at Block and HumanLayer. Its core rule is stated simply: do not let the agent write a single line of code until you have reviewed and approved a detailed written plan.

## Usage

**Research** is a deep read of the codebase producing `research.md`. The survey records a prompting detail from that account — using words like *deeply* and *intricacies* to push the agent toward thorough investigation rather than a first-pass answer.

**Plan** produces `plan.md` as a detailed document carrying code snippets and file paths, refined through one to six *annotation cycles* in which the human adds inline notes in a text editor. The annotation cycle is what makes the approval substantive rather than a rubber stamp: the human's review lands as edits to the plan, not as approval of it.

**Implement** is a batch pass against the approved plan, with type-checking running continuously.

Its distinguishing mechanism is [[DefinedTerm/frequent-intentional-compaction]] at each phase boundary, holding context utilisation in a 40-60% band rather than compacting reactively at 80-100%. The reported result the survey relays is that on a 300k-line Rust codebase this let a team complete a week's worth of work in a day — HumanLayer's own figure rather than an independent measurement.

Its stated fit is mid-size teams, quality-focused projects, and large changes to existing codebases. In the survey's comparison of four workflows, RPI is the one whose verification mechanism is annotation cycles rather than tests or spec conformance, and the one with only medium tool dependency, since it relies on file conventions rather than a framework or plugin.

## Related Terms

RPI is one of four project workflows that survey presents as combinable, alongside a brainstorm-plan-execute flow, [[DefinedTerm/spec-driven-development]], and [[SoftwareApplication/superpowers]]. It shares SDD's insistence on a reviewed artefact before implementation, but the artefact is a plan grounded in a read of the existing codebase rather than a specification of intended behaviour — which is why the survey positions it for brownfield work where SDD is positioned for feature development.
