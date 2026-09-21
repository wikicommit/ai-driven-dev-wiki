---
title: "Test Design"
type: "schema:DefinedTerm"
lang: en
tags: [tdd, ai-assisted-programming]
sources:
  - type: url
    url: 'https://agilejourney.uzabase.com/entry/2025/08/29/103000'
    hash: sha256:3ddb48b38b85526ba30bc0c2f6e032f2041384360d5a6e24c4261f8581fefe0d
    license: all-rights-reserved
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Working out in advance which tests should be carried out against a system — a term from software testing technique and QA practice rather than from TDD vocabulary. In one practitioner's account a model reasons about it usefully only when told which technique to apply, rather than when simply asked to write tests."
---

Test design is deciding in advance which tests should be carried out against a system. Takuto Wada describes it as a term used more in the world of software testing technique than elsewhere, and notes that research into it — working out what verification a given system or specification calls for — is particularly active in Japan, where QA engineers and test engineers use these techniques to decide what to test and how.

Tsutomu Yasui lists, as techniques belonging to test design, equivalence partitioning, boundary value analysis, domain analysis, decision tables, the HAYST method, and pairwise testing.

## Usage

Wada's position is that TDD practitioners do test design too, simply without formalizing it under that name: TDD comes from the programmer's viewpoint, so what is worked through mentally before typing is architecture and data structures, and deciding what to test next is part of that design. He draws the same parallel on the QA side — a test engineer does not start deciding what to test once manual testing is underway, but works out beforehand which groups of functions are effective to test, which are more likely to surface defects, and how to cover the items needing verification in the fewest moves.

Yasui reports that this is the step where prompting makes the difference. Within what he has tried, simply describing what is wanted and asking a model to write tests does not get it to reason logically. Instructing it to use boundary value analysis, to build a particular decision table, or to extract equivalence classes does produce respectable results — his formulation is that making the model use the tools humans use to think logically about test design makes the model think logically too. It is the interviewer, not Yasui, who likens this to prompt engineering.

Yasui adds that a model is also useful for reviewing test design a human produced, and that having a model review a model's test design is not out of the question — but that handing the whole thing over, in the form of "I don't understand any of this, work out the tests", will not go well.

## When It Applies

This is the step the conversation keeps handing back to the human. Generative AI is credited with lowering both the learning cost and the implementation cost of writing tests, and with being strong at [[DefinedTerm/characterization-test]]s that capture existing behaviour, but deciding which tests should be added is treated as a separate question that people work out through test design. The same division is drawn around the [[DefinedTerm/test-list]]: a model can produce something list-shaped and lower the barrier to entering TDD, while what ought to be on the list remains a design judgment.

## Related Terms

[[DefinedTerm/characterization-test]], [[DefinedTerm/test-list]], [[DefinedTerm/red-green-tdd]], [[DefinedTerm/prompt-engineering]]
