---
title: "Semi-Executable Artifact"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-engineering, software-engineering, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.15468'
    hash: sha256:aa9d37128ca41d514105f0cdba213b9927d9c67a443d492554454b40d545252f
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "As defined by Feldt et al., a software-related artifact — such as a prompt, workflow rule, policy layer or organizational routine — that helps specify, coordinate or constrain a system's behavior but whose enactment depends on interpretation by humans, probabilistic models or both, rather than on fully deterministic execution."
---

A semi-executable artifact, as defined in [[ScholarlyArticle/the-semi-executable-stack]], is a
software-related artifact that helps specify, coordinate or constrain the behavior of a
software-intensive system and its surrounding workflow, but whose enactment depends on interpretation
by humans, probabilistic models or a combination of the two, rather than on fully deterministic machine
execution alone. The authors stress that "semi-" does not mean non-executable: such an artifact helps
drive behavior without by itself determining it in the fully specified, deterministic sense of a
classical program, so its execution is approximate, context-sensitive and probabilistic, and may
involve human judgment in some steps. Code is the limiting case of high executability and
organizational routines the limiting case of low executability; prompts, natural-language
specifications, workflow rules, policy layers and decision procedures sit between them, while a purely
informal norm with no stable representational form falls outside the spectrum altogether.

## Usage

The term is the destination concept of the paper's argument that agentic AI expands, rather than
shrinks, the object software engineering works on. Prompts, workflows, policies, evaluation harnesses,
routing logic, escalation rules and decision procedures are, in the authors' words, neither classical
code nor mere documentation: they are read and acted on by models, agents and people at runtime and
therefore shape system behavior as directly as code does. The paper's example is a release-preparation
workflow whose outcome depends not only on code, tests and builds but on prompts that summarize
regressions, orchestration that gathers evidence, evaluation harnesses, escalation rules and a sign-off
routine — and on how well those line up. It points to developer tools such as
[[SoftwareApplication/claude-code]], where prompts, repository instructions, tool permissions and
reusable skills partly encode how work should proceed, as the same pattern in practice.

To reason about where such artifacts sit, the paper arranges them on the Semi-Executable Stack, a
six-ring diagnostic model running from executable artifacts through instructional artifacts,
orchestrated execution, control systems and operating logic to societal and institutional fit, with
outer rings depending more heavily on human interpretation. The practical consequence the authors
draw is that semi-executable artifacts accumulate debt when treated as disposable — a prompt changed
to fix one case silently shifts downstream behavior and no one can later reconstruct why — so
versioning, evaluation suites and traceability from intent to behavior need to be extended to them,
with the same discipline long applied to code.

## Related Terms

- [[DefinedTerm/prompt-debt]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/software-3-0]]
