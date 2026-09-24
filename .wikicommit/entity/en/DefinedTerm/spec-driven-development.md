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
  - type: url
    url: 'https://github.blog/ai-and-ml/generative-ai/spec-driven-development-using-markdown-as-a-programming-language-when-building-with-ai/'
    hash: sha256:26b458e8ba4b8790a046f37bf816d79131b0b7612d69de3ff26ec16690387bb7
  - type: url
    url: 'https://arxiv.org/pdf/2608.30572'
    hash: sha256:c0eb1ba213f36e53531516aecba8c4127b4017c1605a1fac8aba65de8f96ce7d
  - type: url
    url: 'https://arxiv.org/pdf/2601.09745'
    hash: sha256:23e2c28644cabf41082562927407902546dd2d7860f1147ba3e4da97c7ca1f9d
  - type: url
    url: 'https://github.com/engineering4ai/awesome-spec-driven-development'
    hash: sha256:d33ae69c11c61977c4977af54bf7816fa95b5478abcf591af455b4a4693cdf9e
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/sdd/overview/'
    hash: sha256:946cf421ab8284921cee80b48fc236a89feb6dfd5c4a90f01ae072227495be73
  - type: url
    url: 'https://zenn.dev/genda_jp/articles/f71d3ed7d4d7e8'
    hash: sha256:3b930434d815794b112529193eb4b0eb5224288334a07ea828aa21c4e620cc28
  - type: url
    url: 'https://arxiv.org/pdf/2609.00252'
    hash: sha256:5331d1eb219124b67deabb6640416e4b3ac07d3f4ede62ff19407f403d7d576d
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Driving a coding agent from a written task specification rather than directly from a prompt: the prompt is first turned into a specification, which is refined and optionally reviewed by a human, and only then implemented."
---

Spec-driven development is the practice of putting a written specification between a developer's
prompt and an agent's implementation, so that what the agent builds from is a reviewed artefact
rather than the original request. The prompt is first turned into a specification; that
specification is analysed and refined, and can be corrected by a human before anything is built;
implementation then proceeds from the specification and is verified against it. Nine separate
accounts of the practice are described here — a plugin implementation, a third-party account of a
tool vendor's workflow, a practitioner's cross-tool survey, an academic comparison of the frameworks that
implement it, one developer's firsthand account of taking the practice to its limit, a report on
teaching it to undergraduates, an industrial-research case study that pushes the specification
toward formal notation, a Chinese-language handbook chapter that treats the practice as a
question of system determinism, and a post that sets the practice against the standing instruction
files an agent reads every session — and they agree on this much while differing in the concrete
mechanics below.

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

**A fifth account** is one developer's firsthand report rather than a framework or a survey
([[BlogPosting/markdown-as-a-programming-language]]). Writing on the GitHub Blog, Tomas Vesely
describes treating a Markdown file as his application's actual source code and having
[[SoftwareApplication/github-copilot]] compile it into Go, to the point that he rarely edits or
views the generated Go directly. His starting problem is the one the practice exists to address,
reached from the other end: an agent driven by successive prompts loses track of the application's
purpose and past decisions, and a custom-instructions file meant to hold that context goes stale
because updating it duplicates what was already said in the prompt. His answer is to stop treating
the Markdown as instructions accompanying the code and treat it as the code — user-facing
documentation is included by reference into the specification, which that account says keeps
documentation and implementation in sync, and a short, deliberately portable prompt file is what
compiles it. That account describes writing the
specification as programming in Markdown and plain English, with variables, loops and conditions,
and reports that specifications can be linted like code: a second prompt asks the agent to optimize
the specification for clarity, remove duplication and stick to one term per concept. It is a worked
instance of the spec-as-source level the practitioner's survey above sets out, arrived at by
practice rather than argued for.

**A sixth account** comes from a report on introducing the practice into a university team-development
course ([[ScholarlyArticle/sdd-in-software-development-pbl]]). It situates the practice's emergence in
tool-vendor documentation, and summarizes the workflow that documentation sets out: agents executing
requirements analysis, design and implementation planning in sequence, generating a `requirements.md`,
a `design.md` and a `tasks.md` as they go, with developers continuously verifying those documents at
each step to keep them aligned with their intent. On that account the distinguishing feature of the practice is that agents
work from structured specification documents rather than ambiguous natural-language instructions, and
that those documents state architectural patterns, coding conventions, security requirements and
testing strategies explicitly, which the agent then treats as constraints. It notes that many agents,
[[SoftwareApplication/github-copilot]] among them, pick up such workflows and project rules from
Markdown custom-instruction files — a `copilot-instructions.md` in that course's case. Its own
adaptation collapses requirements analysis and design into a single investigation phase, on the
reasoning that this generalizes the workflow to feature additions and debugging rather than only new
requirements, and adds an explicit review phase in which agent and developer confirm the implementation
matches the specification.

**A seventh account** comes from an IBM Research case study
([[ScholarlyArticle/enhancing-formal-software-specification-with-artificial-intelligence]]) that pushes
the specification toward formal notation rather than toward tooling. Its authors write the
specification as natural language augmented with lightweight mathematical notation in LaTeX, treating
it as an intermediate representation between informal requirements and fully formal specification
languages, and have the model review it for ambiguities and inconsistencies before any code is
generated. That account reports the review-before-generation ordering as the source of its gain: the
same program specified this way took about a sixth of the time of correcting an implementation
iteratively from its execution results, and was correct on the first generation attempt. It also
describes permitting the model to work in the manner of this practice on the surrounding program —
formalizing the problem in intermediate Markdown files before implementing — and reports that doing so
made visible which decisions the model had taken about elements outside the business logic.

**A curated index** of the practice's tooling, *Awesome Spec-Driven Development*, maintained on GitHub
by Engineering4AI, is worth less for any single entry than for the shape it gives the ecosystem. It
sorts projects into introductions, standards, specification tools, development frameworks, IDE and
editor integrations, MCP servers, workflow management and related lists. Those categories separate
questions the practice's own literature tends to run together. Its Standards section holds
[[DefinedTerm/agents-md]], which it describes as a Markdown-based format for specifying agent
behaviour, alongside [[DefinedTerm/first-principles-framework]], which it describes instead as a
rigorous framework for modelling systems, methods and knowledge with auditable assurance levels.
Separate from those sit the tools that author a specification ([[SoftwareApplication/github-spec-kit]],
[[SoftwareApplication/openspec]]), the frameworks that wrap a whole development workflow around one
([[SoftwareApplication/bmad]]), the IDE and editor integrations that build the practice into the
editor ([[SoftwareApplication/kiro]]), and the boards and orchestrators under workflow management that
track work spanning several specifications at once. Its own one-line gloss on the practice — comprehensive specifications created before implementation begins,
which it says improves alignment between requirements and delivery, code quality, testing and
documentation — sits at the level of generality the accounts above share. Each entry in it is a name
and a sentence, so it is evidence of how the tooling has spread and how practitioners categorise it,
not of how any particular tool works.

**An eighth account** is a chapter of Jimmy Song's online handbook 智能体构建指南, and what is
distinctive in it is that it makes accuracy a question of system determinism. Its definition is
close to the others' — a structured specification as the single source of truth driving design,
implementation, testing and deployment, written in natural language or structured Markdown as an
executable contract stating what the software should do and why — and it positions SDD against TDD
and BDD by saying it moves the vantage point further forward still, settling what and why before
implementation is entered at all. Where it differs is in what it says accuracy depends on: *high
accuracy is not the model's cleverness but the system's determinism*, reached by constraining the
model with rules, feeding it through context, and reusing experience as workflows.

That account puts figures on when the practice is worth it, offered as evaluation criteria rather
than as measurements: it holds that a code-generation system with a success rate below 50% costs more
in rework than it returns in productivity, and gives target values of at least 90% of output
compiling and running directly, at least 85% passing automated tests, and at most 10% needing manual
repair — with a task type becoming a production capability rather than an experiment once it holds
above 90%. Its account of the automated pipeline is the familiar Specify → Plan → Tasks → Implement →
Deploy loop, with build, static analysis and test suites acting as the verification oracle and
failures fed back so the model re-plans and retries until the correctness conditions hold.

Two framings in it are not in the accounts above. The first is a three-layer protocol stack it says
turns AI from a point assistant into a member of the system:
[[DefinedTerm/model-context-protocol]] defining how the AI interacts with tools,
[[DefinedTerm/agent2agent-protocol]] letting agents collaborate, and AG-UI establishing real-time
visible interaction between user and agent. The second is an adoption principle it calls **AI First
in Non-Business Domain**: start where tasks are high-frequency, already have clear rules and are
decoupled from core business — its examples are retiring A/B experiments, configuration cleanup and
security fixes — and expand to business innovation only after automation is working in that
controlled range. It names the same problems others do as the reason — context drift, uncontrollable
results, no standard for collaboration between human, AI and tools — but answers them with a
sequencing rule rather than with gates or artefact rigor.

This chapter is a section of an online handbook rather than a study, and states no evaluation of its
own; its accuracy targets and its adoption principle are given as positions rather
than as measured findings.

A further account approaches the practice from outside it, asking how a feature specification relates
to the standing instruction files an agent reads at the start of every session.
[[BlogPosting/division-of-labor-in-ai-instruction-files]] sets the two side by side and finds the same
commitments underneath — write before implementing, hold machine-readable and human-readable content
together, give the agent persistent context to consult, constrain syntax to reduce ambiguity, and fix
decisions in a known place — while separating them by time axis. On that post's reading a
specification scoped to a single feature is created for it, consumed by it, and archived once the
feature is done, whereas files such as [[DefinedTerm/agents-md]] and [[DefinedTerm/design-md]]
describe standing norms that are maintained and grow. That is a characterisation of the
feature-scoped spec's lifecycle in the tools it names, and sits alongside rather than displaces the
accounts above in which an approved specification is kept as a versioned artefact and fed back into
later sessions.

Its example of syntax constraining ambiguity is Kiro's use of EARS notation — Easy Approach to
Requirements Syntax — which it describes as a writing convention that shapes a requirement into one
of five fixed templates. The connection it proposes between the two kinds of file
is that a feature spec could reference a design token defined in a standing `DESIGN.md` instead of
restating it, which it offers as a way to avoid maintaining the same norm in two places. It states that this is not yet a
widely established practice.

**A further account treats the practice as a team-level discipline** rather than as a workflow for
one developer and one agent. [[ScholarlyArticle/spec-driven-development-for-agentic-software-engineering]]
defines it through four commitments a team makes: every non-trivial planned change originates from a
written specification treated as the contract for that change; the specification is version-controlled
alongside the code under the same review, audit and rollback discipline; code, tests, documentation and
infrastructure are derived from it, by humans, agents or both, with explicit provenance back to it; and
when specification and artifact disagree, the specification is the source of truth, the disagreement
being resolved by re-deriving the artifact or amending the specification, never by silent edits. It
separates two levels of specification — system specifications, which describe the durable architecture,
conventions and normative rules and are materialized in the rule files an agent loads every session, and
feature specifications, which describe one change and are archived once it is delivered — and warns
that loading only the feature level yields functionally correct but architecturally inconsistent code,
while loading only the system level leaves the agent unable to ground the task. It further distinguishes
both from skills, which are procedural and loaded on demand rather than normative and always active.

That account rejects two readings of the practice: that it means more documentation (specifying before
implementation is presented as an act of design, whereas documenting existing code lags behind it) and
that it implies a waterfall process (iteration is kept, but happens over specifications first and code
second, as in a proposal–apply–archive cycle). It pairs the practice with a
[[DefinedTerm/methodological-harness]] of team-owned mechanisms built around the specification, and it
presents the whole as a conceptual framework drawn largely from gray literature, whose predicted
benefits are hypotheses rather than findings. It also limits its own scope: for exploratory work whose
requirements are genuinely unknown, it suggests a lighter discipline may be more appropriate.

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

The framework comparison is the account that foregrounds one risk most directly: where the
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

The firsthand account adds the limits a single practitioner runs into rather than ones a framework
anticipates. Writing the specification is reported as sometimes harder than writing the code
directly, because it demands describing precisely what is wanted; compilation slows as the
generated code grows, and that account's stated next step is to have the specification instruct the
agent to split each section into its own module. Its author had not added tests at the time of
writing, and states that testing remains essential even in spec-driven workflows, since a
specification describes intended behaviour while tests verify it.

The IBM Research case study contributes a boundary of a different kind: which parts of the program the
specification must pin down. Its authors argue that a system analyst has to separate what the model may
modify from what it must preserve — peripheral elements such as a user interface can be left to the
model, while anything touching business logic should come back to the analyst for confirmation,
particularly where the intention is ambiguous. They demonstrate the cost of getting that line wrong by
summarizing their own precise specification into loose prose and regenerating from it, and report that
the reconstruction dropped or corrupted several things the original had fixed, among them the notion of
separate organizations, the ordering of events, and a bound on one actor's budget. That account also
reports an attention limit rather than a conceptual one: past a few pages, the model occasionally
omitted parts of the specification during generation, which its authors read as an argument for
decomposing longer specifications.

How well established the practice is, none of these accounts settles on their own. The seven treated
in this paragraph each use the
term for its own implementation or account of the pattern; the context-engineering-kit's reliability
claims — including that its plugin produced working code in every case its team tested — are the
project's own, based on internal production use rather than independent evaluation. The GitHub Spec
Kit account comes from a third-party blog post drawing on the tool's own documentation and on a
separate GitHub analysis of agent instruction files, rather than from an independent evaluation of
Spec Kit itself. The practitioner's survey is likewise
a self-published technical report rather than a peer-reviewed study; its case studies are presented
as illustrative examples, and the error-reduction figures it cites for human-refined specifications
are drawn from other studies it references rather than from its own measurement. The framework
comparison is a preprint by a single author, and it is explicit that its dimensional scores are that
author's judgement from each framework's official documentation rather than an independently validated
measurement, assigned by a single rater with no second coder and no inter-rater reliability reported.
It also declares a conflict of interest, one of the frameworks it scores being its own author's.
The sixth account is an implementation report on a single university course with four teams, so what
it says is a description of one adaptation of the practice rather than an evaluation of the practice
in general. The firsthand account is the narrowest evidence of those seven: one developer's experience of a few
months on a single personal project, published by the vendor whose coding agent it uses, and
offered by its author as an experimental workflow rather than a recommendation. The seventh is an
industrial-research case study reporting one team's experience on a single simulation program, with its
timing comparison drawn from the authors' own two attempts rather than from a controlled study.

## Related Terms

- [[DefinedTerm/vibe-coding]] — the practice the project contrasts its plugin with: it describes
  the plugin as not a vibe-coding solution while noting that out of the box, driven from a single
  prompt with no human checkpoints, it behaves like one
- [[DefinedTerm/subagent-driven-development]] — the lighter-weight approach the same project offers
  as a distilled version of this one
- [[DefinedTerm/llm-as-a-judge]] — the evaluation technique used for the quality gates between
  phases
- [[BlogPosting/good-spec]] — source of the GitHub Spec Kit account of this practice
- [[BlogPosting/markdown-as-a-programming-language]] — source of the firsthand account above, in
  which a Markdown file is treated as the application's source code and the generated Go is rarely
  edited directly
- [[ScholarlyArticle/from-code-to-contract]] — source of the three-tier specification-rigor spectrum
  (spec-first, spec-anchored, spec-as-source) and the Specify/Plan/Implement/Validate workflow
  presented above
- [[DefinedTerm/three-tier-boundaries]] — a related spec-writing pattern set out in the good-spec
  post above, not in the survey
- [[ScholarlyArticle/from-prompt-to-process]] — source of the fourth account above, comparing the
  frameworks that implement this practice
- [[DefinedTerm/six-dimension-process-taxonomy]] — the instrument that comparison uses, under which
  specification is the field's least discriminating dimension
- [[DefinedTerm/reverse-documentation-engineering]] — the inverse direction, recovering specifications
  from legacy code rather than writing them for new work
- [[ScholarlyArticle/sdd-in-software-development-pbl]] — source of the sixth account above, reporting
  on teaching the practice in an undergraduate team-development course
- [[ScholarlyArticle/enhancing-formal-software-specification-with-artificial-intelligence]] — source of
  the seventh account above, in which the specification is written in natural language augmented with
  mathematical notation and reviewed by the model before any code is generated
- [[SoftwareApplication/agentscript]] — one of the implementations the eighth account lists, in
  which the agent's own plan is emitted as code rather than as prose
- [[ScholarlyArticle/spec-driven-development-for-agentic-software-engineering]] — source of the
  team-level account above, with its four commitments and its two levels of specification
- [[DefinedTerm/methodological-harness]] — the set of team-owned mechanisms that account builds around
  the specification
