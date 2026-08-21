---
title: "Test-Driven AI Agent Definition"
type: "schema:DefinedTerm"
lang: en
tags: [testing, spec-driven-development, agent-evaluation, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.01160'
    hash: sha256:5df903e44f8c186d0b13aaf412c53e475ccd30551e159a2cbba53b5c0a79dd50
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A four-stage pipeline, credited to Rehan (2026), in which a behavioural specification is compiled into a test suite by one coding agent, a second agent refines the agent prompt until the tests pass, and mutation testing validates the tests themselves."
  termCode: "TDAD"
  inDefinedTermSet: ""
---

Test-Driven AI Agent Definition — abbreviated TDAD — is a pipeline for defining an AI agent's behaviour by compiling a natural-language specification into executable tests and then refining the agent's prompt until it passes them. The account here comes entirely from [[ScholarlyArticle/productivity-reliability-paradox]], which credits the pipeline to Rehan (2026) and evaluates it as an instantiation of the [[DefinedTerm/specification-governance-model]]'s executable-contract mechanism.

## Usage

The pipeline as described has four stages. A natural-language behavioural specification defines the agent's expected behaviour. A coding agent — [[SoftwareApplication/claude-code]] running in Docker — generates pytest test cases from that specification. A second coding agent iteratively refines the agent prompt until all tests pass. Finally, mutation testing validates the test suite itself, checking that the tests can actually distinguish a correct implementation from an incorrect one.

The human role in this arrangement is confined to specification authorship and mutation-score review. In the taxonomy that same paper proposes, this is what Test-Driven Development becomes at the autonomous-agency tier: the core principle that tests drive design is preserved, while human effort relocates from writing tests to governing specifications.

Reported outcomes, across four domains and 24 experimental trials, are compilation success rates of 92% (v1) and 58% (v2), mean hidden-test pass rates of 97% (v1) and 78% (v2), mutation scores of 86–100%, and 97% mean regression safety under specification evolution. The paper's reading of these figures is that the mutation scores validate the governance mechanism itself as reliable, and that regression safety shows specification evolution not degrading dependability.

Its stated limitation is scope. Compared with [[SoftwareApplication/spec-kit]], which operates at the feature level across the full lifecycle, TDAD operates at the level of agent behaviour: its strength is formal verifiability through mutation testing, but it addresses agent prompt quality rather than the upstream specification process that determines what the agent should do in the first place. The paper's proposal is to combine both — a feature-level specification pipeline feeding an agent-level verification pipeline — as a layered governance architecture where each level constrains the one below.

## Related Terms

TDAD is one of two evaluated instantiations of the [[DefinedTerm/specification-governance-model]], alongside [[SoftwareApplication/spec-kit]], and sits at Tier 3 of the [[DefinedTerm/ai-augmented-methodology-taxonomy]]. It is a specific answer to the circular-validation risk that arises when [[DefinedTerm/spec-driven-development]] lets the same generator write both tests and implementation.
