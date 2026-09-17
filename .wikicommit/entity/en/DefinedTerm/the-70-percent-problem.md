---
title: "The 70% Problem"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/agentic-engineering/the-70-percent-problem/'
    hash: sha256:53a2beb793aa9395530c062c1818c57e7d558905d0e21444c19b239b602f7997
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "As framed in Addy Osmani's agentic-engineering glossary, the observation that AI coding tools reliably produce a working first draft covering roughly 70% of a task, while the remaining 30% (edge cases, security, accessibility, integration) takes longer and requires engineering judgment AI can't reliably supply on its own."
---

The 70% problem, as framed in Addy Osmani's agentic-engineering glossary, is the observation that AI coding tools reliably generate a working first draft — structure, boilerplate, happy-path logic, standard patterns — covering roughly 70% of a task almost immediately, while the remaining 30% (the null-instead-of-empty-array edge case, a race condition that only appears under load, an ignored accessibility requirement, a security vulnerability hidden behind plausible-looking code, an awkward integration point) takes longer than the first 70% did and requires engineering judgment that AI can't reliably supply on its own.

## Usage

The source presents the 70% problem as the reason agentic engineering exists as a discipline: if AI could reliably deliver the full 100%, no engineering practice would be needed around it. Recognizing the gap changes how an engineer allocates their time, shifting effort from writing code to reviewing, testing, handling edge cases, and integrating it — described as a fundamentally different, and arguably harder, skill than writing code from scratch. The 70% problem is framed as applying mainly to production-bound code; AI is described as excelling at prototypes, where the 70% is often sufficient. Better prompts, specs, and context are said to push the AI-covered share from 70% toward 80–85%, but the source states that closing the full gap still requires human engineering judgment. It also frames junior developers who only know how to reach the 70% mark as less valuable on a team than senior engineers who can efficiently close the remaining 30%.

## Related Terms

The source names this term alongside [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/comprehension-debt]], [[DefinedTerm/skill-atrophy]], and [[DefinedTerm/ai-assisted-code-review]] as related glossary/blog entries, without defining any of them.
