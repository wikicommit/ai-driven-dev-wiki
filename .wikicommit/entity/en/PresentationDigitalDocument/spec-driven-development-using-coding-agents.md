---
title: "Spec-Driven Development Using Coding Agents"
type: "schema:PresentationDigitalDocument"
lang: en
tags: [spec-driven-development, ai-assisted-programming, agentic-coding]
sources:
  - type: url
    url: 'https://www.jfokus.se/jfokus26-preso/Spec-driven-Development-using-Coding-Agents.pdf'
    hash: sha256:826071b0039518cb28ef1798aa3d05619a61db6492c48424db207313c18d6363
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A conference slide deck by Arun Gupta arguing that vibe coding is a one-shot approach that produces unmaintainable results, and presenting spec-driven development as the intention-first alternative, illustrated throughout by an analogy between building a backyard and building software."
  author: "[[Person/arun-gupta]]"
  datePublished: ""
  recordedAt: ""
  url: "https://www.jfokus.se/jfokus26-preso/Spec-driven-Development-using-Coding-Agents.pdf"
---

"Spec-Driven Development Using Coding Agents" is a conference slide deck by [[Person/arun-gupta]], presented in his capacity as VP, Developer Experience at JetBrains. It argues that [[DefinedTerm/vibe-coding]] is a one-shot approach whose output cannot safely be extended or changed, and presents [[DefinedTerm/spec-driven-development]] as the intention-first alternative — with the specification, not the code, as the source of truth.

The deck is structured as an extended analogy. It opens by describing what happens when you "vibe code" a backyard: a prompt like "just build me something cool for grilling" leaves the contractor to assume your intention, so the barbecue arrives with no cutout in the stone for it, and the result is a vibe that looks fine on the surface but fails on the first "production" dinner because the plumbing and gas line were never connected. It then re-runs the same project from a blueprint, and maps each element of that construction process onto a software development lifecycle before moving on to the practical mechanics — `AGENTS.md`, Agent Skills, implementation plans, and the drift problem.

## Key Points

- **Vibe coding is a one-shot approach.** The deck's stated consequences are no structure, no planning, lots of hallucinated files, misunderstanding of the codebase, ignorance of corporate standards, code that is hard to extend and nearly impossible to safely change once the original mental model is gone, and code that is harder to review. Its summary of the problem is that vibe coding generates code based on your vibe, and that what is needed instead is "an intention-first, code-second approach." Citing the DORA report, it adds that AI tends to amplify existing organizational strengths or weaknesses: good teams get better, struggling teams may get worse.

- **The backyard-to-codebase mapping.** Blueprint maps to the specification (API, DB schema); resource lock to interface definition; utility dependencies to infrastructure such as auth, DB and API gateways; sub-contractors to specialized agents for test generation, security and docs; contractor validation loops or permits to self-correction loops such as a linter or test suite; and building a second backyard to reusing the same spec across Java, Go and Python. The slogan attached to the blueprint is "the blueprint is the source of truth," and the one attached to the investment argument is "run slow to run fast."

- **What spec-driven development is, in the deck's terms.** Write natural-language specifications defining what and why — intent (desired behavior), interfaces (contracts between components), requirements (functional and non-functional), and acceptance criteria in Gherkin format. Review and refine those specs independent of implementation, have AI agents generate and validate code against them, and let human judgment define the "what" while AI efficiency delivers the "how."

- **A four-stage spec-driven SDLC.** Research (existing codebases and patterns, technical papers and best practices, agent-generated research reports, stakeholder interviews, dependencies and integration points); Standardize (rules such as linting, ADRs and style guides; skills; MCPs and integrations; project structure and conventions); Define (scope boundaries, requirements, contracts, UI/UX, testing strategy and acceptance gates); and Loop (AI-driven code generation from specs, continuous validation against specs, iterative refinement between code and spec, and traceability and change management).

- **Making specs reusable and testable.** The deck lists seven properties of a reusable spec: clear scope boundaries ("in scope" versus "out of scope" to prevent feature creep), documented ADRs with rationale, language and framework agnosticism, structured requirements separating functional from non-functional, a contract-first approach with JSON schemas defined upfront, acceptance criteria as testable WHEN/THEN conditions, and tech stack recommendations offered as guidance rather than prescription. To make specs unambiguous it recommends Given-When-Then acceptance criteria per requirement, replacing soft words like "typically," "expected," "strategic," and "best" with imperatives and measurable values — its worked example replaces "Prioritizes moves," "Recommends," and "Considers" with "MUST select moves in this priority order" plus exact numeric priorities — and defining error codes, schemas, explicit data types and constraints for every failure case.

- **Implementation plans and validation gates.** The deck describes an implementation plan as the output of transforming a spec through a prompt, and lists the qualities it should have: direct traceability to spec requirements, phased incremental delivery, optimization for AI efficiency (small, well-scoped units fit in context windows and drift less from intent), validation gates with a "Definition of Done" between phases, comprehensive testing planned rather than added as an afterthought, quantified success metrics, built-in risk mitigation, and dependency and resource tracking.

- **Agent drift and UI/UX.** For design work the deck's recommendation is to bridge existing tools to agents over MCP — copying a Figma selection link into an agent to generate a `ui-spec.md`, then referencing that spec in `AGENTS.md` for UI work — while noting the long-term requirement for communication between the design team and the developer when designs change.

- **Three separations and three practices.** Its closing summary states the three separations of SDD as separating thinking from doing (specs define "what," agents define "how"), separating strategy from tactics (review specs, not lines of code), and separating patterns from projects (build portable skills, not one-off prompts); and the three practices that matter as investing upfront to accelerate delivery, building in phases with gates, and letting the AI interview you to arrive at better specs. Its final line is that AI amplifies what you already have, so it is worth making sure you are amplifying the right things.

## Context

The deck's own one-sentence definition of the practice is worth recording as a summary of its position: spec-driven development is "writing down what your AI should know (AGENTS.md), what it should do (skills), and what you're building (implementation plan), so you can stop explaining and start building." That framing makes the deck's two practical mechanisms — [[DefinedTerm/agents-md]] and [[DefinedTerm/agent-skills]] — load-bearing rather than incidental.

It also surveys the state of the field rather than presenting a settled method. Under "what's happening in spec-driven development space" it names Spec-kit, AgentOS, Kiro, AntiGravity and Tessl as emerging tools and reports growing adoption across greenfield and brownfield projects, then lists open questions it does not answer: how SDD integrates with TDD, BDD and DDD; who maintains specs as code evolves; and how multiple agents coordinate on parallel work. Drift prevention strategies and multi-agent orchestration patterns are named as the next challenges.
