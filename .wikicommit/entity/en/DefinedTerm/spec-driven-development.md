---
title: "Spec-driven development"
type: "schema:DefinedTerm"
lang: en
aliases: ["SDD", "Specification-driven development"]
tags: [agents, coding-tools, llm, long-horizon-tasks]
sources:
  - type: url
    url: https://github.com/NeoLabHQ/context-engineering-kit
    hash: sha256:3a00d5fa6029f48343ba32101feda4acd0f31870b7ff74ef954be99d4e04a584
    license: GPL-3.0
  - type: url
    url: 'https://addyosmani.com/blog/good-spec/'
    hash: sha256:fbb1e0c078b1d920689cbc3c652ad4bf253d5b39c77f957cab7ee4e6cd1ff5fa
  - type: url
    url: https://arxiv.org/pdf/2602.00180
    hash: sha256:982804fd917021d4811f4b23fc3ada9dfc07e4c91add2e07b32b2ffa9aad4253
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Driving a coding agent from a written task specification rather than directly from a prompt: the prompt is first turned into a specification, which is refined and optionally reviewed by a human, and only then implemented."
---

Spec-driven development is the practice of putting a written specification between a developer's
prompt and an agent's implementation, so that what the agent builds from is a reviewed artefact
rather than the original request. The prompt is first turned into a specification; that
specification is analysed and refined, and can be corrected by a human before anything is built;
implementation then proceeds from the specification and is verified against it. Four independent
accounts of the practice are described here — a plugin implementation, a tool-vendor-published
workflow, a practitioner's cross-tool survey, and an academic comparison of the frameworks that
implement it — and they agree on this much while differing in the concrete mechanics below,
including how many levels of rigor the practice is understood to have.

## Usage

**The Spec-Driven Development plugin in [[SoftwareApplication/context-engineering-kit]]** reduces the
practice to three commands: one creates a task file from an initial prompt, one analyses the prompt
and iteratively refines the specification until it meets a quality bar, and one produces a working
implementation from the resulting file and verifies it. The project characterises the result as
development as compilation — task specification in, working code out — and suggests clearing the
agent's session between planning and implementation so the second step starts on a fresh context.
Planning is split across specialised sub-agents for research, codebase exploration, requirements and
acceptance criteria, architecture, and decomposition into independently verifiable steps;
implementation runs per step, with review at the end of each phase. Its specification format is
based on arc42, which the project calls a widely adopted standard for software development
documentation, adjusted for what an LLM can act on by removing parts the project judges to add
nothing to implementation quality. Around the core loop sit optional refinements: a `--refine` flag
to re-run planning after a human has edited or commented on the specification, a
`--human-in-the-loop` flag to gate each planning and implementation phase, and the ability to declare
dependencies between tasks so that a large piece of work can be decomposed into separately specified
units.

**GitHub's Spec Kit**, described in a separate source, structures the same core idea as four gated
phases — Specify, Plan, Tasks, Implement — where a human does not move to the next phase until the
current one is validated. Specify covers user journeys and success criteria rather than technical
stack; Plan is where the developer supplies architecture, stack, and constraints for the agent to turn
into a technical plan; Tasks breaks the spec and plan into small, independently reviewable and
testable chunks; and Implement works through those tasks one by one (or in parallel), with the
developer reviewing focused changes rather than large code dumps at the end. That source frames the
specification, once approved, as a persistent, version-controlled artefact fed back into the agent's
context across sessions, comparable to a team's Product Requirements Document.

**A third account**, from a 2026 practitioner's survey of spec-driven development
([[ScholarlyArticle/from-code-to-contract]]), frames SDD as a spectrum of three levels of rigor
rather than a single practice: **spec-first**, where a specification guides only the initial
implementation and may be left to drift once code exists; **spec-anchored**, where the specification
is maintained alongside the code throughout its lifecycle, with automated checks — often tests
derived from the spec — keeping the two synchronized; and **spec-as-source**, where the specification
is the only artefact developers edit directly and code is entirely generated and regenerated from it,
as already established in domains like Simulink-based embedded-systems development. That survey
describes a four-phase workflow common across the tools it examines — Specify, Plan, Implement,
Validate — with human review at each phase boundary, and names [[SoftwareApplication/github-spec-kit]],
[[SoftwareApplication/kiro]], and [[SoftwareApplication/tessl]] as representative AI-assisted
toolkits spanning the spectrum.

**A fourth account**, from an academic comparison of frameworks supporting AI development agents
([[ScholarlyArticle/from-prompt-to-process]]), approaches the practice from the outside: rather than
describing one workflow, it scores six such frameworks against a
[[DefinedTerm/six-dimension-process-taxonomy]] and reports what they have in common. It frames the
underlying movement as converting the prompt into a contract — the initial instruction is only a
starting point, and the real work begins when it becomes a PRD, specification, plan, story, task,
architecture or checklist, which is what creates review points and reduces ambiguity. Within that
movement it distinguishes full and lightweight variants, placing [[SoftwareApplication/github-spec-kit]],
[[SoftwareApplication/openspec]] and [[SoftwareApplication/spec-kitty]] as variations of the same move
at different levels of overhead. Specification is the dimension on which almost every framework it
scored rates highest, which is why that study calls it the field's common denominator and the
dimension that discriminates between frameworks least. It also names the complementary extreme:
[[DefinedTerm/reverse-documentation-engineering]], which recovers specifications from existing systems
instead of writing them for new ones.

## When It Applies

The practice trades developer time and tokens for reliability, so it applies where that trade is
worth making. The context-engineering-kit project positions it for complex or large codebases with
existing structure — arguing that, unlike frameworks aimed at greenfield work, it performs better the
more existing code there is, because each planning phase includes an analysis of which files a
change would affect and which patterns to follow. Its own comparison places the specification-driven
route at the reliable end of a progression that starts with a one-shot prompt, and puts the token
overhead at a multiple of the baseline, rising further with human review.

It assumes that a specification is worth writing at all, and that the developer will invest in it.
The context-engineering-kit project is explicit that quality is highly proportional to the time spent
iterating on the specification, and that without human feedback the result will be working but
sub-optimal — by default the plugin makes its own assumptions rather than asking for clarification,
on the reasoning that developer time is more valuable than model time. The failure mode it reports is
not a broken build but wasted effort: when the initial specification was wrong because of missing
information or task complexity, the agent still self-corrected to a working solution, but took much
longer and spent time on wrong paths, which is why it advises decomposing work into smaller tasks and
reviewing each specification independently.

The GitHub Spec Kit account frames the same trade differently: its four gated phases exist to prevent
what that source, citing Simon Willison, calls "house of cards code" — fragile AI output that
collapses under scrutiny — by refusing to let implementation start until the spec and plan are
validated. In that account's Plan phase specifically, a company's standardized technology choices,
legacy-integration constraints, or compliance requirements are what the developer supplies for the
agent to fold into the technical plan.

The framework comparison adds a risk the other three accounts do not foreground: where the
specification becomes a source of truth, it has to stay aligned with the code, and drift between
specs, plans, tasks, tests and implementation is the first of the recurring risks it maps across the
frameworks it examined. Its proposed answer is not a practice but a research agenda — automatically
detecting when a code change invalidates a specification, and measuring intermediate artifact quality
rather than only the final result.

The practitioner's survey account gives its own decision framework: SDD is worth adopting for
AI-assisted development generally, for complex requirements, for systems with multiple maintainers,
for integration-heavy systems, for regulated domains needing traceability, and for legacy
modernization; it considers the overhead unjustified for throwaway prototypes, solo short-lived
projects, exploratory coding, and simple applications with obvious requirements.

How well established the practice is, none of the four sources settles on their own. Each uses the
term for its own implementation or account of the pattern; the context-engineering-kit's reliability
claims — including that its plugin produced working code in every case its team tested — are the
project's own, based on internal production use rather than independent evaluation. The GitHub Spec
Kit account comes from a third-party blog post citing GitHub's own published study and documentation
of the tool, rather than from an independent evaluation of it. The practitioner's survey is likewise
a self-published technical report rather than a peer-reviewed study; its case studies are presented
as illustrative examples, and the error-reduction figures it cites for human-refined specifications
are drawn from other studies it references rather than from its own measurement. The framework
comparison is a preprint by a single author, and it is explicit that its dimensional scores are that
author's judgement from each framework's official documentation rather than an independently validated
measurement, assigned by a single rater with no second coder and no inter-rater reliability reported.
It also declares a conflict of interest, one of the frameworks it scores being its own author's.

## Related Terms

- [[DefinedTerm/vibe-coding]] — the practice the project contrasts its plugin with: it describes
  the plugin as not a vibe-coding solution while noting that out of the box, driven from a single
  prompt with no human checkpoints, it behaves like one
- [[DefinedTerm/subagent-driven-development]] — the lighter-weight approach the same project offers
  as a distilled version of this one
- [[DefinedTerm/llm-as-a-judge]] — the evaluation technique used for the quality gates between
  phases
- [[BlogPosting/good-spec]] — source of the GitHub Spec Kit account of this practice
- [[ScholarlyArticle/from-code-to-contract]] — source of the three-tier specification-rigor spectrum
  (spec-first, spec-anchored, spec-as-source) and the Specify/Plan/Implement/Validate workflow
  presented above
- [[DefinedTerm/three-tier-boundaries]] — a related spec-writing pattern from the same source
- [[ScholarlyArticle/from-prompt-to-process]] — source of the fourth account above, comparing the
  frameworks that implement this practice
- [[DefinedTerm/six-dimension-process-taxonomy]] — the instrument that comparison uses, under which
  specification is the field's least discriminating dimension
- [[DefinedTerm/reverse-documentation-engineering]] — the inverse direction, recovering specifications
  from legacy code rather than writing them for new work
