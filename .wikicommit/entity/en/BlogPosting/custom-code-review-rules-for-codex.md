---
title: "Custom Code Review rules for Codex"
type: "schema:BlogPosting"
lang: en
tags: [code-review, agent-config, coding-agents]
sources:
  - type: url
    url: 'https://developers.openai.com/blog/custom-code-review-rules-for-codex'
    hash: sha256:545da2cc607e493ec8565ebfedabe86da5990d39d08e426344d54fa68908973a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An OpenAI developer blog post announcing that Codex Code Review can apply custom repository rules written in AGENTS.md and cite them in its findings, with OpenAI's advice, drawn from its own evaluations and internal use, on how to write rules that help rather than add noise."
  author: ["Hari Srikanth"]
  datePublished: "2026-07-20"
  publisher: "[[Organization/openai]]"
---

This post announces that [[SoftwareApplication/codex-code-review]] can use custom repository rules in [[DefinedTerm/agents-md]] to catch recurring issues and point authors to the guidance behind a finding. Its starting observation is that some review comments keep coming back — preserving an older API contract, keeping customer data out of logs, avoiding a rename that would break another service — and that these checks are easy to miss when the context lives with a handful of reviewers. Teams that already use `AGENTS.md` to guide coding tasks can use the same file to guide reviews.

The motivation it gives is volume. Coding agents are taking on larger, longer-horizon changes, and the post reports that weekly PR volume at OpenAI has more than doubled since Q4, with similar trends at many customers. More pull requests, it argues, means reviewers have less time to work out what each change does and gather context, so code review becomes the [[DefinedTerm/review-bottleneck]] — and some problems cannot be seen from the diff alone, such as a field rename that looks like routine cleanup but breaks clients depending on the existing contract.

The post's worked example comes from the Codex repository itself: its `AGENTS.md` holds a breaking-change review rule naming an experimental app-server notification that Codex Cloud already consumes, so that a one-line rename which still compiles would draw a finding telling the author to keep the name or add a backward-compatible event.

## Key Points

- Repository rules are described as "an interface": concise, scoped review guidance kept in `AGENTS.md`, which Codex Code Review can apply to a change and cite in a finding instead of the same explanation being repeated in every pull request.
- Rules are scoped by location: repository-wide rules at the root, service-specific rules in the relevant directory's nested `AGENTS.md`, so an unrelated change does not pull in context it does not need.
- Rules are positioned as complementing tests and linters rather than replacing them: deterministic checks belong in those tools, while repository rules capture the judgment that is harder to encode; compatibility requirements and data boundaries are named as good places to start.
- OpenAI reports an eval suite with known rule violations and safe counterexamples in which rule-guided variants recovered 98% of the required custom findings, compared with 58.3% for the baseline control; results were organized around coverage, restraint, retention of ordinary bug-finding, and actionability.
- The post reports from both testing and internal repositories that broad instructions easily create noise, while small, scoped rule sets with an explicit safe path helped Codex focus.
- Its four writing rules: start with a consequential, non-obvious invariant (if removing a rule would not change the review, leave it out); scope rules to the code they govern; state the invariant and the safe path; and keep rules durable and current by describing outcomes rather than function names, and by narrowing or removing rules that repeatedly produce noise.
- Formatting and other mechanical checks are to stay in CI; repository rules are for the questions a reviewer would otherwise have to ask again.
- To test a rule, the post suggests one change that should trigger it, one safe counterexample and one unrelated change, checking that only the first produces a finding.
- Codex Code Review is described as still an additional reviewer: tests, branch protections and required approvals continue to provide hard enforcement.

## Context

The post is OpenAI documenting a feature of its own product, and the evaluation figures are OpenAI's internal results rather than an independent measurement. Its framing ties the feature to a broader claim about agent-driven development — that faster code production shifts the constraint to review — which is shared by other writing in this wiki on [[DefinedTerm/agentic-code-review]].
