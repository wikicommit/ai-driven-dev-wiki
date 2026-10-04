---
title: "Adopting spec-driven development in a multi-team organization"
type: "schema:HowTo"
lang: en
tags: [spec-driven-development, team-organization, requirements]
sources:
  - type: url
    url: 'https://github.com/zhangluka/SDD'
    hash: sha256:2af3b4894634ee5c3441ff3bf53a97026520c2679b2851f6aa9a072fc620c496
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5"
generated_with: "0.9.0"

properties:
  description: "A phased procedure for introducing spec-driven development into an organization where several teams work from Word requirement documents and separate design documents, by inserting a reviewed, structured specification with testable acceptance criteria into the existing process and making it the single source of truth before adding automation."
---

This procedure introduces [[DefinedTerm/spec-driven-development]] (SDD) into an organization that already runs a conventional process — business analysts write requirements in Word and clarify them in meetings, developers write an overall design and a detailed design that are reviewed with analysts and testers, then code, test and deliver — and where several teams build parts of the same requirement. It comes from a Chinese-language practice guide whose approach is not to replace that process but to insert a structured specification layer into it and let that specification gradually become the single source of truth for every role.

The guide's diagnosis is that requirements (in Word), design (in another document), code and test cases are separate sources that drift apart, clarifications often live only in meeting minutes, and acceptance criteria sit in testers' heads or scattered spreadsheets — gaps that widen when several teams read the same requirement differently.

## Prerequisites

- A shared location that every team involved can access and that is versioned with the code, such as a `specs/` directory in a Git repository.
- A pilot project or business line with clear requirement boundaries and a manageable timeline.
- Analysts, developers and testers — and operations or security where relevant — willing to take part in specification reviews.

## Steps

1. **Pilot with a specification step.** After the existing requirement-clarification meeting, have its output be a structured specification for the requirement rather than meeting minutes. The analyst drafts it from the Word document and the clarification results, with developers and testers adding boundaries, exceptions and how each criterion will be checked. Use a fixed template (Markdown or Word) that requires a specification ID, name and business goal; scope, stating what is and is not included; inputs, outputs and rules as lists or tables rather than prose; success, failure, boundary and exception cases; and acceptance criteria, each written as "given X, the system should Y, verifiable as Z". The specification states only what is to be done and how it is accepted — not technology choices, class names, table structures or algorithms, which belong in the design. Review it with the analyst, developers and testers; passing review freezes it as the binding basis for the iteration. Then require design documents and task tickets to state which specification they implement, and test cases to map to its acceptance criteria. The pilot's purpose is to check whether specification-first reduces rework and aligns understanding across roles.
2. **Bind the specification to design and code.** Add a check to design reviews that every acceptance criterion in the specification is covered, and require the specification ID on merge requests, pull requests or task tickets — manually at first, with scripts later. Once the pilot is stable, write the template and the review exit criteria up as internal operating instructions and extend them to more teams.
3. **Make the specification the basis for acceptance and close-out.** Use the specification and its acceptance criteria as the checklist for user acceptance and project close-out instead of the Word document or verbal agreements, and require that any later change first updates and re-reviews the specification before development is scheduled.
4. **Add machine readability and automation.** Only after two or three teams are developing against specifications, move the template to a structure a script can parse — YAML or JSON, or Markdown with fixed headings — and add lightweight tooling: generating acceptance checklists from specifications, linking specifications to tasks and test cases, and a CI or gate check that a change touching a module has a corresponding specification with a recent review. The guide suggests a simple command-line tool that validates specification format and lists the tasks and pull requests linked to a specification ID, rather than a heavyweight platform.

## Notes

**Multiple teams.** Create specifications per requirement or feature, not per team, with one specification ID per requirement shared across teams. When several teams implement one specification (for example a back-end interface and a front-end view), split its acceptance criteria by module or interface so each team's design and tasks cite the same specification and their own criteria. Write cross-team interfaces — APIs, events and data, with inputs, outputs, error codes and key constraints — into the specification as contracts, and notify every team implementing a specification whenever that specification changes. Specification reviews should bring together a representative from each team.

**Existing deliverables.** The Word requirements document stays as the analyst's input and background, but the binding basis moves to the structured specification; overall and detailed designs stay but must cite the specification ID and come after it; clarification meetings stay but their output becomes an updated specification; and acceptance checklists align with the specification's criteria.

**AI coding.** The guide recommends giving the AI the relevant part of the specification and its acceptance criteria as context for the current task, and reviewing generated code against whether it conforms to the specification and covers the listed criteria. On tools, the guide concludes that teams following it should prefer [[SoftwareApplication/github-spec-kit]], or Speck where Claude Code is the main tool, adding [[SoftwareApplication/openspec]] where strong contracts and executable acceptance are needed.

**Judging success.** The guide suggests looking at whether core features have reviewed specifications, whether requirement changes, bug fixes and refactors update the specification first (checked by sampling pull requests and tickets), whether specifications trace to tasks and code and back, whether rework and production defects fall for comparable requirements, and — where AI is in use — whether generation tasks that take a specification as input succeed first time more often.
