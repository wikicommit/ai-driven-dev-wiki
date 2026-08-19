---
title: "LLM-as-Judge"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, code-quality, agent-architecture]
sources:
  - type: url
    url: 'https://github.com/NeoLabHQ/context-engineering-kit'
    hash: sha256:bc2a9a7e51d46faa7b71b485a040ec8d6f6b10a78fc25f17a65dc7b9dde39b4c
  - type: url
    url: 'https://code.claude.com/docs/en/best-practices'
    hash: sha256:92807ef3d58f63fbea435ea928df49e2f3341e118eb8c40db08800c100a4c4c5
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The pattern of using a separate model invocation to evaluate work another model produced, scoring it against a rubric or set of criteria so the evaluation is not made by the same context that generated the output."
  termCode: ""
  inDefinedTermSet: ""
---

LLM-as-Judge is the pattern of using a separate model invocation to evaluate work another model produced. Its defining property is separation: the judge sees the output and the criteria, not the reasoning that produced the output, so the agent doing the work is not the one grading it. In agentic coding it typically appears as a quality gate — a step that must pass before work is accepted, with a failure feeding back into a retry.

## Usage

[[SoftwareApplication/context-engineering-kit]] uses the pattern as its named mechanism for quality gates, describing them as evaluating each planning and implementation step using evidence-based scoring against predefined verification rubrics. Its commands expose several shapes of it: `/judge` evaluates completed work against structured rubrics; `/do-and-judge` pairs an implementation subagent with an independent judge and an automatic retry loop until the work passes; `/judge-with-debate` runs iterative multi-judge debate, either building consensus or reporting the disagreement; and `/critique` runs a multi-perspective review using specialised judges with debate and consensus building. Its review plugin applies a related idea with role-specialised reviewers — bug hunting, code quality, contracts, historical context, security, and test coverage — filtered by impact and confidence.

Anthropic's Claude Code documentation describes the same separation without the label, framing it as adding an adversarial review step: before treating a task as done, have a subagent review the diff in a fresh context and report gaps. Its stated rationale matches the pattern's premise — a reviewer running in a fresh context sees only the diff and the criteria it is given, not the reasoning that produced the change, so it evaluates the result on its own terms — and it notes the practical benefit that the implementing session receives the gaps directly and can fix and re-review without a human copying findings between windows.

That documentation also records the pattern's most common failure mode: a reviewer prompted to find gaps will usually report some even when the work is sound, because that is what it was asked to do, and chasing every finding leads to over-engineering — extra abstraction layers, defensive code, and tests for cases that cannot happen. Its recommended mitigation is to tell the reviewer to flag only gaps affecting correctness or the stated requirements and treat the rest as optional.

## Related Terms

LLM-as-Judge is the model-based counterpart to [[DefinedTerm/backpressure]], where the rejection mechanism is a deterministic tool such as a compiler or test suite rather than another model; the two are usually combined. It is the review gate in [[DefinedTerm/subagent-driven-development]], is implemented using [[DefinedTerm/subagents]], and is one form of the agentic quality control that [[Report/2026-agentic-coding-trends-report]] predicts will become standard as AI-generated output outpaces human review capacity.
