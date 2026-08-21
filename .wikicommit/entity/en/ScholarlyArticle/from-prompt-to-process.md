---
title: "From Prompt to Process: a Process Taxonomy and Comparative Assessment of Frameworks Supporting AI Software Development Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [spec-driven-development, taxonomy, agentic-coding, framework-comparison]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A comparative study proposing a six-dimension process taxonomy — specification, context, roles, execution, validation and portability — and applying it with a three-point rubric to six frameworks that structure work around AI coding agents."
  author: ["Sanderson Oliveira de Macedo"]
  datePublished: "2026-06-04"
  abstract: "Selects six frameworks supporting AI software development through a directed search with functional inclusion and traction criteria, proposes a six-dimension process taxonomy with a scoring rubric, and finds convergence on persistent artifacts and review points alongside a structural trade-off between process depth and portability across agents."
  keywords: ["AI software development", "AI agents", "specification", "software engineering", "agentic frameworks", "comparative study of frameworks"]
  citation: ""
---

This paper, by Sanderson Oliveira de Macedo of the Federal Institute of Goiás, examines what it calls *frameworks supporting AI software development* — defined as a structured set of artifacts, commands, roles, templates, workflows or policies that runs over an agent to organise whoever uses it. Its stated gap is that recent surveys map agents and LLMs for software engineering by tasks, benchmarks and internal components, but no study centres on the operational frameworks that turn those capabilities into process; and that comparing frameworks by number of agents, number of commands or repository stars fails to capture the function each mechanism plays in the engineering process.

Its hypothesis is that the value of these frameworks lies less in automating code writing than in how they structure the cognitive and operational work around the agent — so that the question shifts from "which model writes better code?" to "which process lets humans and agents keep context, traceability and control over changes?"

Six frameworks were selected by a directed search of primary sources with a functional inclusion criterion and a traction measurement: [[SoftwareApplication/spec-kit]], [[SoftwareApplication/openspec]], the [[SoftwareApplication/bmad-method]], [[SoftwareApplication/get-shit-done]], [[SoftwareApplication/spec-kitty]] and [[SoftwareApplication/reversa]].

## Key Contributions

**A six-dimension process taxonomy**, each dimension stated as a guiding question:

- **Specification** — how does intention become a work contract? Its weak extreme is a bare prompt; its strong extreme a versioned set of requirements, acceptance criteria, plans, tasks, architecture and policies.
- **Context** — how does the agent know what is relevant? Repository, docs, hooks, rules, memory, evidence, gaps.
- **Roles** — who decides, who implements and who reviews? Personas, agents, skills, responsibilities, authority.
- **Execution** — does the framework act on the environment or only guide? Code editing, commands, tests, browser, terminal, IDE.
- **Validation** — how are errors detected before becoming deliverables? Tests, checklists, gates, artifacts, human review, confidence.
- **Portability** — does the process survive outside one tool? Multiple integrations, open formats, lock-in, local installation.

The paper treats the six as complementary reading lenses rather than disjoint partitions, so the same feature may score in more than one dimension — its example being worktree isolation, which is execution while the required review before merge is validation.

**A three-point scoring rubric** turning the taxonomy into a replicable instrument: 0 where a dimension is absent or incipient, 1 where partial, 2 where strong or central to the framework's design. Applied to the six frameworks it yields BMAD Method 10, Spec Kitty 9, GitHub Spec Kit 8, OpenSpec 6, Reversa 6, and GSD 4, out of a maximum of 12.

**Two headline findings.** Among frameworks that already adopt some process there is convergence: the isolated prompt loses centrality, and persistent artifacts, work contracts, traceability and human review become the mechanisms that reduce ambiguity and coordinate agents. And **no framework scores 2 across all six dimensions**, which the paper reads as a structural trade-off — the most portable frameworks sacrifice roles and validation, the deepest-process one reduces portability and execution, and the most context-focused one zeroes roles, validation and portability. In direct answer to its first research question, the dimensions that most discriminate between frameworks are roles and validation, while specification, being nearly universal, distinguishes little.

**Five cross-cutting patterns** are named in the comparative discussion: the conversion of the prompt into a contract; context treated as an engineering asset, whose absence produces "functional hallucinations" — code that compiles but violates implicit contracts; validation beyond the final test, because an agent can pass tests while improperly altering the architecture or removing a business constraint; the tension between autonomy and governance, where the relevant question is not whether agents can execute but under which policies, permissions and evidence; and the emergence of an agent supply chain.

**A map of recurring risks**: drift between specification and code, excessive trust in generated artifacts, fragility of community extensions, platform dependence, and a lack of benchmarks for the complete process.

## Notes

The scoring is explicitly the author's judgement from each framework's official documentation, not an independent empirical measurement — the paper states this directly beneath its own results table.

An out-of-sample check applies the taxonomy to Spec-Flow, a specification-driven toolkit for Claude Code deliberately excluded from the sample for low traction at roughly 85 stars. It scores 11 of 12 — the most complete profile of any case examined — which the paper uses to argue two things at once: that the taxonomy generalises beyond its sample, and that adoption and process completeness are orthogonal, confirming the limitation of using traction as a proxy for maturity. The author accepts the methodological consequence: the object set is the most *adopted* frameworks, not the most complete ones by the instrument.
