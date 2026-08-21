---
title: "AI-Augmented Methodology Taxonomy"
type: "schema:DefinedTerm"
lang: en
tags: [methodology, taxonomy, spec-driven-development, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.01160'
    hash: sha256:5df903e44f8c186d0b13aaf412c53e475ccd30551e159a2cbba53b5c0a79dd50
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A two-dimensional classification proposed by Farrag (2026) of how six established software development methodologies transform across three tiers of AI integration, from passive suggestion through active generation to autonomous agency."
  termCode: "AAMT"
  inDefinedTermSet: ""
---

The AI-Augmented Methodology Taxonomy — abbreviated AAMT — is a classification proposed in [[ScholarlyArticle/productivity-reliability-paradox]] of how established software development methodologies are modified when AI agents are introduced. Its stated motivation is a gap: the paper argues that no peer-reviewed work had produced a rigorous taxonomy of methodology transformation, with the TDD-with-LLM and BDD-with-LLM literatures existing as isolated streams and earlier taxonomies classifying tool types or interaction modalities rather than methodological impact.

## Usage

The taxonomy has two dimensions. The first is an **AI integration tier**, defined by the degree of AI autonomy in the software development lifecycle:

- **Tier 1, Passive Suggestion.** The AI provides inline completions the developer accepts or rejects. The developer retains full control and the AI is a productivity accelerator within an unchanged methodology. Named examples are the original Copilot and Tabnine.
- **Tier 2, Active Generation.** The AI generates complete functions, test cases or documentation from natural-language descriptions within developer-defined constraints. The developer's role shifts from author to reviewer, and the methodology must accommodate review-intensive workflows. Named examples are ChatGPT-assisted coding, Copilot Chat, and Claude in conversational mode.
- **Tier 3, Autonomous Agency.** Agents autonomously execute multi-step workflows including file creation, test execution, debugging and iterative refinement with minimal human intervention. The developer's role shifts from reviewer to *governor*, and the methodology must supply specification and verification structures that constrain autonomous execution. Named examples are [[SoftwareApplication/claude-code]], Cursor Composer, Copilot Workspace, and Devin.

The second dimension is **methodology**: six are analysed — Test-Driven Development, Behavior-Driven Development, Domain-Driven Design together with Domain-Driven Testing, Agile, Waterfall, and DevOps.

The worked TDD case shows what the taxonomy is meant to expose. At Tier 1 the AI auto-completes during the Green phase, accelerating implementation while leaving the test-writing discipline intact. At Tier 2 it generates tests and implementation together, which the paper argues inverts the discipline — tests stop being the driver of design and become co-generated artefacts — so that the TDD *principle* (tests constrain generation) survives while the *practice* (a human writes tests first) transforms; the risk it names is circular validation, where AI-generated tests mirror AI-generated code. At Tier 3 the [[DefinedTerm/test-driven-ai-agent-definition]] pipeline is offered as the agentic evolution, confining the human role to specification authorship and mutation-score review.

The paper qualifies the taxonomy's own use. Most teams do not follow a single methodology in pure form — a typical team combines Agile cadences with selective TDD, informal BDD scenarios and CI/CD automation, spanning several cells at once — so the AAMT is presented as an analytical decomposition rather than a description of how teams self-identify. Its stated value is helping practitioners isolate which methodological dimension of a hybrid practice a given integration tier most affects, and therefore where governance investment should be concentrated.

## Related Terms

The AAMT is one of four contributions of the paper that also proposes the [[DefinedTerm/productivity-reliability-paradox]] and the [[DefinedTerm/specification-governance-model]]; the tier that most needs governance in its account, Tier 3, is the territory of [[DefinedTerm/agentic-coding]] and [[DefinedTerm/spec-driven-development]].
