---
title: "Spec-Driven Development"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, terminology, software-development-process, specification]
sources:
  - type: url
    url: 'https://github.github.com/spec-kit/concepts/sdd.html'
    hash: sha256:8eb0247a43c5afbc5b75f447d9f90202cdd390cf55fa951daad26cb7eedbad2f
  - type: url
    url: 'https://arxiv.org/pdf/2602.00180v1'
    hash: sha256:982804fd917021d4811f4b23fc3ada9dfc07e4c91add2e07b32b2ffa9aad4253
  - type: url
    url: 'https://kiro.dev/blog/introducing-kiro/'
    hash: sha256:83f496f2e0d7f844907485218708133937302b71468f8cc11cabc239a5753da9
  - type: url
    url: 'https://github.com/NeoLabHQ/context-engineering-kit'
    hash: sha256:bc2a9a7e51d46faa7b71b485a040ec8d6f6b10a78fc25f17a65dc7b9dde39b4c
  - type: url
    url: 'https://sddbook.blob.core.windows.net/downloads/spec-driven-development.pdf'
    hash: sha256:7f897827f00db69ac4a15f3acea3826e5504b1600d0b785cdce210d5414f1eea
  - type: url
    url: 'https://en.wikipedia.org/wiki/Spec-driven_development'
    hash: sha256:c3223384adaa004ab0eb9bf49d5fc63239f56bea0f4d628a75fee609d90a24e2
  - type: url
    url: 'https://www.jfokus.se/jfokus26-preso/Spec-driven-Development-using-Coding-Agents.pdf'
    hash: sha256:826071b0039518cb28ef1798aa3d05619a61db6492c48424db207313c18d6363
  - type: url
    url: 'https://aws.amazon.com/blogs/industries/from-spec-to-production-a-three-week-drug-discovery-agent-using-kiro/'
    hash: sha256:88a7c9517554f4f93af74e1fddd0380527eccaa4427916af91e6ffd946845cff
  - type: url
    url: 'https://specstory.com/whitepapers/beyond-code-centric-specstory-2025.pdf'
    hash: sha256:4dc1c2f09b2ea2dff0c8bfb3cc6e5eb177c4c5134a96a0025cf03ad6841972e8
  - type: url
    url: 'https://developer.microsoft.com/blog/spec-driven-development-ai-native-engineering/'
    hash: sha256:4f50523f95a4cb4f60ff352214d2246d274b6f50c67967a56174d96b51f8d4ed
  - type: url
    url: 'https://arxiv.org/pdf/2605.01160'
    hash: sha256:5df903e44f8c186d0b13aaf412c53e475ccd30551e159a2cbba53b5c0a79dd50
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
  - type: url
    url: 'https://arxiv.org/pdf/2606.27045'
    hash: sha256:9004fd8330acfa64f27d8cc588f1234dd91b29303e4ee479b537bbdebca481f6
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A development approach that inverts the traditional relationship between specification and code by treating the specification as the source of truth and code as a generated or verified secondary artifact. Concrete implementations vary in how much authority the spec holds over the code, from guiding an initial build to being the only artifact humans edit."
---

Spec-Driven Development (SDD) is a development approach that inverts the traditional relationship between specifications and code: the specification becomes the source of truth, and code is derived from, generated from, or verified against it rather than being the de facto record of what the system does. [[ScholarlyArticle/spec-driven-development-from-code-to-contract]] states the core principle directly — in spec-driven development, code is the implementation detail of the specification, not the other way around; the spec declares intent and the code realizes it.

The motivation given is a diagnosis of code-centric practice. Requirements documents exist but drift; design diagrams are drawn but rot; tests are written but often after the fact — so the code, whatever it actually does, becomes the de facto truth of the system. When a stakeholder asks whether the system meets requirements, the answer requires reverse-engineering intent from implementation. The rise of AI coding assistants has made this newly consequential: an assistant asked to add a feature must guess what the developer wants from a vague prompt, and the result is often plausible-looking code making dozens of unstated assumptions.

[[Book/spec-driven-development-ai-native-software-engineering]] states the same inversion in operational terms: instead of prompting and fixing, you write specifications, and instead of maintaining code you maintain the specs that generate it — so that, in its author's phrasing, "the specification becomes the artifact. Code becomes a side effect." [[Person/kevin-ryan]] presents SDD as an emerging discipline still in flux rather than a finished canon, and argues the idea is being arrived at independently across the industry by practitioners starting from very different places; what is missing, on his account, is a shared language and a shared set of practices rather than a new invention.

## Usage

Concrete implementations of the idea differ mainly in how much authority the specification holds over the code, and correspondingly how much discipline is required to keep the two aligned. Piskala's report organizes this as a [[DefinedTerm/specification-spectrum]] with three named levels — spec-first, where the spec guides an initial build and may then be abandoned; spec-anchored, where the spec is maintained alongside the code and synchronization is enforced by tests; and spec-as-source, where the spec is the only artifact humans edit and code is regenerated rather than hand-edited. The report identifies spec-anchored as the level that suits most production systems, and states a rule of thumb it calls the Golden Rule: use the minimum level of specification rigor that removes ambiguity for your context.

The same report proposes a four-phase workflow that it presents as common across SDD approaches regardless of tooling: **Specify** (what to build), **Plan** (how to build it), **Implement** (build it), and **Validate** (verify it), with human review at each checkpoint and each phase producing an artifact that constrains the next.

Individual toolkits instantiate this idea in their own ways. The [[SoftwareApplication/spec-kit]] documentation presents Spec-Driven Development as a structured process emphasizing four things: intent-driven development, where specifications define the "what" before the "how"; rich specification creation using guardrails and organizational principles; multi-step refinement rather than one-shot code generation from prompts; and heavy reliance on advanced AI model capabilities for specification interpretation. It sets out three development phases:

| Phase | Focus | Key activities |
| --- | --- | --- |
| 0-to-1 Development ("Greenfield") | Generate from scratch | Start with high-level requirements, generate specifications, plan implementation steps, build production-ready applications |
| Creative Exploration | Parallel implementations | Explore diverse solutions, support multiple technology stacks and architectures, experiment with UX patterns |
| Iterative Enhancement ("Brownfield") | Brownfield modernization | Add features iteratively, modernize legacy systems, adapt processes |

The same documentation states the research and experimentation behind its approach focuses on technology independence — validating the hypothesis that Spec-Driven Development is a process not tied to specific technologies, programming languages, or frameworks — along with enterprise constraints such as organizational cloud providers, tech stacks, engineering practices, design systems and compliance requirements; user-centric development across different user cohorts; and creative and iterative processes including parallel implementation exploration, iterative feature development, and upgrade and modernization tasks. Spec Kit does not prescribe how teams preserve or mutate the `spec.md`, `plan.md`, and `tasks.md` artifacts after requirements change; its documentation covers that separately under spec persistence models and the evolving-specs workflows for existing projects.

[[SoftwareApplication/kiro]] implements the idea inside an IDE, with a three-step sequence its announcement calls building with specs: a single prompt is unpacked into user stories whose acceptance criteria are written in EARS (Easy Approach to Requirements Syntax) notation, making the prompt's assumptions explicit; a design document follows from the codebase plus the approved requirements, producing data flow diagrams, interfaces, database schemas, and API endpoints; and tasks are then generated, sequenced by dependency, and linked back to individual requirements, each carrying its own test, accessibility, and responsiveness details. Its distinguishing claim among these implementations is bidirectional synchronisation — developers can write code and ask Kiro to update the specs, or edit specs manually to refresh the tasks — offered against the failure mode where the original artifacts stop being updated during implementation.

[[SoftwareApplication/context-engineering-kit]]'s SDD plugin places the same idea in a plugin for command-line agents, built on the arc42 documentation standard adjusted for LLM capabilities. Its workflow is three commands — `/add-task` to create a task file from an initial prompt, `/plan-task` to research and refine it into a specification, and `/implement-task` to produce and verify an implementation — with each phase run by role-specialised agents (researcher, code-explorer, business-analyst, software-architect, tech-lead, developer, code-reviewer, tech-writer) and gated by [[DefinedTerm/llm-as-judge]] scoring. Its maintainers describe the goal as "development as compilation" (task specs → run the command → working code), and, unusually among these implementations, claim it performs *better* on large existing codebases than on greenfield work, because each planning phase includes a codebase impact analysis step. They also state that quality is proportional to time invested in refining the specification, and that human review of the specification is the single most effective improvement available — a `--human-in-the-loop` flag exists for exactly this.

[[Person/arun-gupta]] presents the same inversion as a practitioner argument in [[PresentationDigitalDocument/spec-driven-development-using-coding-agents]], reached through an analogy between building a backyard and building software: a prompt-and-pray request produces something that looks acceptable on the surface and fails in use, whereas a blueprint fixes exact dimensions and interfaces up front and becomes the source of truth. His definition of the practice is to write natural-language specifications defining what and why — intent, interfaces, requirements, and acceptance criteria in Gherkin format — review and refine them independently of implementation, and have agents generate and validate code against them, with human judgment defining the "what" and AI efficiency delivering the "how." He organises the resulting lifecycle into four stages, Research, Standardize, Define and Loop, and argues the up-front cost pays for itself, in the slogan "run slow to run fast."

His account is unusual among these implementations in specifying what makes a spec *reusable* rather than merely correct: clear in-scope and out-of-scope boundaries to prevent feature creep, documented architecture decisions with their rationale, language and framework agnosticism, functional and non-functional requirements separated, a contract-first approach with schemas defined upfront, acceptance criteria as testable WHEN/THEN conditions, and tech stack recommendations offered as guidance rather than prescription. On unambiguity his prescription is concrete — replace soft language such as "typically," "expected," "strategic," and "best" with imperatives and measurable values, and define error codes and schemas for every failure case — and his worked example is replacing "Prioritizes moves" with "MUST select moves in this priority order" plus exact numeric priorities.

Other implementations sit at different points on the spectrum. Piskala's report describes model-based design with Simulink as spec-as-source in practice — engineers verify control algorithms at the model level and generate certified C code that nobody hand-edits — and describes API-first development with OpenAPI plus contract testing as a spec-anchored pattern in which the spec becomes the contract that frontend and backend teams can develop against in parallel.

Where AI coding agents are involved, the report argues specifications act as "super-prompts" that break complex problems into modular components aligned with agents' context windows, and that partitioning work at the spec level lets multiple agents implement different components simultaneously without interference. It reports that empirical studies, though nascent, suggest human-refined specs significantly improve LLM-generated code quality, with controlled studies showing error reductions of up to 50%.

Ryan's book proposes scaffolding for the same idea rather than a tool. Its methodology has three parts: a Five Artefact taxonomy — spec, code, provenance, scenarios and tests — as the structure for specification quality, a builder-tester agent separation as the model for execution, and a provenance chain for traceability. It frames the practical target using [[DefinedTerm/five-levels-of-vibe-coding]], arguing that the fully autonomous [[DefinedTerm/dark-factory]] at Level 5 requires infrastructure most organisations cannot justify while Level 3 or 4 is achievable, and that the new bottleneck sits in two places: specification quality — describing what needs to exist precisely enough that a machine can build it without a human filling gaps — and AI-native execution, the pipelines, agent workflows, evaluation systems and deployment gates that turn a specification into running software and validate the result. Ryan's stated reason for the first of these is that a specification which works for a human developer, who can ask questions and use judgment to resolve ambiguity, does not work for an AI agent: "The agent will do what you say. If what you said was imprecise, the output will be precisely wrong."

### A reported end-to-end application

[[BlogPosting/three-week-drug-discovery-agent-using-kiro]] is a dated practitioner account of the method run through one project, and its value here is that it states both the artifacts and the reason for them. Its contrast is drawn against [[DefinedTerm/vibe-coding]], which it characterises as "the iterative, exploratory approach where developers write code directly based on intuition and immediate needs, refining through trial and error" — workable for small prototypes but, on its account, hard to scale while ensuring quality and consistency. Spec-driven development, "by contrast, separates planning from execution."

The reason the post gives for that separation is where the human sits. Of four advantages it lists, it calls this the most important: the approach "maintains human-in-the-loop oversight at the planning stage", so a misreading of intent is caught and corrected in the requirements, design and tasks documents before execution begins, which it says prevents costly rework. The other three are the context the specifications give the tool to implement features autonomously while developers review and validate; onboarding, since new team members can read the specs to learn what was built and why; and reuse, since a team can ask for "a new feature based on the previous implementation with the same tech stack".

Its reported outcome for one project — three developers, three weeks, more than 95% of business logic code generated, over 80 hours of development time and an estimated 8 hours of documentation time saved — is the vendor team's own figure for its own tool, published by AWS, with no independent verification. Its stated recommendation is nonetheless method-level rather than tool-level: define clear acceptance criteria with stakeholders before writing any code, front-load steering documents capturing architecture decisions, coding standards and integration patterns, and connect [[DefinedTerm/model-context-protocol]] knowledge sources to improve generation accuracy.

### A practitioner's qualification

[[Report/beyond-code-centric]], a whitepaper by [[Person/greg-ceccarelli]] of [[Organization/specstory]], arrives at the approach from the same premise as the accounts above — agents can implement well given solid specifications, humans remain indispensable for design, prioritization and judgment, and the gap between English-language specification and code is narrowing — but stops short of endorsing it as ready. Its stated position is that the approach redistributes complexity rather than removing it, demanding mastery of micro-decisions that seasoned developers otherwise handle by intuition: what context to load before a prompt, which model suits which stage, and which scope assumptions must be made explicit that humans would leave unspoken. Its conclusion is a qualified one — "until we create better intent-centric tools that reduce these micro-decisions, spec-driven development with agents remains powerful in theory but insufficient in practice" — with the practical advice that teams should distinguish frictional micro-decisions from high-leverage macro-decisions and "spend energy shaping architecture, not typing file paths". Its own named implementation of the approach is [[DefinedTerm/specflow]].

### Translation loss as the stated motivation

[[BlogPosting/spec-driven-development-a-spec-first-approach-to-ai-native-engineering]], a Microsoft developer-blog post of June 2026 by [[Person/apoorv-gupta]], motivates the approach from a different starting point than the code-drift diagnosis above: **translation loss**, the erosion of meaning as an idea moves through the delivery lifecycle. It locates that loss at four specific handoffs — stakeholder needs to product requirements, requirements to architecture and design, design to implementation, and implementation to validation and release — and argues that "without a shared artifact that preserves intent, every handoff becomes an interpretation step." Its sharpest formulation of what AI does and does not change is that "AI can accelerate those steps, but it cannot correct ambiguity that was never resolved."

Its case against prompt-first workflows is correspondingly about durability rather than quality: prompt-first works for simple tasks, but when requirements, constraints, and edge cases live only in prompts, teams get fast output with no durable source of truth, which the post says produces architectural drift, code drift, inconsistent implementations, harder reviews, and rework. The reallocation it describes is of effort rather than of total time — more spent clarifying intent and planning up front, less lost to downstream rework, with test shifting earlier because acceptance criteria are explicit from the start.

One of its stated lessons cuts against maximal adoption of the practice, and its adoption playbook adds cautions in the same direction — both worth keeping alongside the spectrum above. The lesson is that "not every change needs the full lifecycle, so adoption should be right-sized"; the playbook recommends piloting on a single feature where alignment problems are already visible, keeping the process lightweight at first, treating specs as living artifacts, avoiding over-specification too early, and expanding only where value is clear. Its compact statement of the dependency the whole practice rests on is "Spec quality = output quality." These are first-party lessons from a vendor advocating its own toolkit, reported qualitatively; the three project outcomes the post gives — including onboarding time cut from two to three weeks to a few days in one brownfield project — come with no methodology.

### An economic argument for why it emerges

[[ScholarlyArticle/productivity-reliability-paradox]] argues that specification discipline is not a stylistic preference but the economically rational governance response to a specific set of transaction attributes, and proposes the [[DefinedTerm/specification-governance-model]] to formalise that claim. Its reasoning is that AI-mediated code production combines high asset specificity (generated code has limited value outside its intended architecture and codebase), high behavioural uncertainty (non-deterministic generators that violate unstated conventions without intent), and high frequency (dozens to hundreds of invocations a day), and that this combination makes heavy upfront specification investment the optimal choice under Transaction Cost Economics — because frequency amortises the fixed cost of building the governance structure.

The same paper's thesis statement is the strong form of the claim: "specification discipline, not model capability, is the binding constraint on AI-assisted software dependability." It also gives specifications a second, non-economic rationale — as compressed, persistent representations of project context (architectural rules, API contracts, invariants) that can be included in every invocation, partially compensating for a model's finite context window.

### Convergence across frameworks, and what it does not settle

[[ScholarlyArticle/from-prompt-to-process]] compares six frameworks that structure work around coding agents and reports convergence in mechanism: among frameworks that already adopt some process, "the isolated prompt loses centrality, and persistent artifacts, work contracts, traceability and human review become mechanisms that reduce ambiguity and coordinate agents." It names this pattern *from prompt to contract* — the initial instruction becomes only a starting point, and the real work begins when it becomes a PRD, specification, plan, story, task, architecture or checklist.

Its dimensional scoring qualifies how much that convergence explains. Specification is the most saturated of its six dimensions, with almost all frameworks scoring the maximum, which makes it the common denominator of the field but a poor discriminator between tools; roles and validation are the polarised dimensions that actually distinguish them. And no framework in the set scores strongly on all six dimensions, which the paper reads as a structural trade-off between process depth and portability across agents rather than a gap current tools have already closed.

Two of its other cross-cutting patterns bear directly on the practice. Context is treated as an engineering asset, whose absence produces what it calls *functional hallucinations* — code that compiles but violates implicit contracts. And validation must extend beyond the final test, because an agent can pass the tests while improperly altering the architecture, removing a business constraint, or ignoring a product decision; the paper's stated consequence is that evaluation must measure not only whether the final answer works but whether the path to it was auditable.

The paper also records the inverse direction as a legitimate case, through [[SoftwareApplication/reversa]]: many real environments are brownfield, where the problem is recovering operational contracts from existing systems rather than writing specifications for new ones.

### A middle ground between spec-first and spec-as-source

[[ScholarlyArticle/the-spec-growth-engine]] positions its own proposal against two extremes it argues both fail. *Spec-first* frameworks generate full specifications before any code, at the cost of upfront overhead and the risk of specifying the wrong thing. *Spec-as-source* systems generate code from specifications, which it says introduces nondeterminism and a fragile single point of truth that teams consistently reject in practice. Its stated middle ground is to be spec-anchored — every node has a specification — while remaining code-coupled, with code and specification evolving in the same commit, and drift-enforced, so that divergence is a blocking merge error rather than a discipline problem.

Its growth protocol is a two-layer rule rather than a single ordering. Layer 1 — root invariants and key container boundaries such as persistence, security, external integrations and the error taxonomy — is specified before any feature and is deliberately *not* just-in-time, forming a floor below which architecture cannot silently erode. Layer 2 grows as hardest-first vertical slices. The paper's argument is that this blocks two orderings that each fail on their own: breadth-first, where hard problems hide in stubs and surface only at the end, and pure agile with no floor, where a needed boundary never appears because no feature happened to force it — which it names as the origin of many hardcoded workarounds in production systems.

The same framework treats [[DefinedTerm/spec-code-drift]] as the failure mode that determines whether any of this survives contact with an agent, and its stated remedy is structural rather than procedural: the agent updates the affected specification in the same commit as the code, and the human reviews only contract-level changes.

## Related Terms

Piskala's report positions SDD as an evolution rather than a revolution, characterizing Test-Driven Development as SDD at the unit level and Behavior-Driven Development as the most direct ancestor of modern SDD, and quoting Bryan Finster's observation that "SDD is not a revolution... it's just BDD with branding". It argues the branding still serves a purpose: reminding practitioners that specs should be authoritative rather than advisory. Under its user-centric development goal, the Spec Kit documentation lists supporting various development approaches ranging from [[DefinedTerm/vibe-coding]] to AI-native development.

The name also predates the AI-era usage. Wikipedia's article on specification-driven development gives a much broader definition — a software development approach in which specifications are used to develop software — and places it in a family it calls documentation-driven development, alongside model-driven development, model transformation, and round-trip engineering. It records one earlier line of work in particular: Ostroff, Makalsky, and Paige present an agile approach to specification-driven development that combines features of test-driven development with the plan-based approach of design by contract, describing tests and contracts as different types of specifications that are useful and complementary for developing software. The article's "see also" list — behavior-driven development, design by contract, formal methods, model-driven engineering, test-driven development — is the same neighbourhood Piskala's ancestry argument places the modern term in, arrived at independently of the AI framing.

Several implementations define themselves explicitly against vibe coding. Kiro's announcement illustrates its position with a Venn diagram placing Kiro itself in the overlap between "the flow of vibe coding" and "the clarity of specs", and states that Kiro is great at vibe coding but goes beyond it to get prototypes into production. Context Engineering Kit's maintainers put the relationship more sharply: their plugin "is not a 'vibe coding' solution, but out of the box, it works like one" — running from a single prompt to the end of a task and making evidence-based assumptions rather than repeatedly asking for clarification, on the reasoning that developer time is more valuable than model time — with the caveat that quality is sub-optimal when no human feedback is supplied. Where specification-writing is instead deferred and generated in parallel with implementation, see [[DefinedTerm/subagent-driven-development]].
