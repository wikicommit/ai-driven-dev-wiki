---
title: "Doom Loop"
type: "schema:DefinedTerm"
lang: en
tags: [agent-failure-modes, harness-engineering, agentic-coding]
sources:
  - type: url
    url: 'https://blog.langchain.com/improving-deep-agents-with-harness-engineering/'
    hash: sha256:7628e7920b4c219963d45c07cb27a6039a14ef5a60f3939b0ccb424dd7481ddd
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A failure mode of coding agents in which an agent, having committed to a plan, keeps making small variations on the same broken approach instead of stepping back to reconsider it."
---

A doom loop is a failure mode in which a coding agent, having settled on a plan, repeatedly makes small
variations to the same broken approach rather than reconsidering it. LangChain, in
[[BlogPosting/improving-deep-agents-with-harness-engineering]], attributes it to agents being myopic once
they have decided on a plan, and reports seeing the same approach retried ten or more times in some of its traces.

## Usage

LangChain uses the term in the context of [[DefinedTerm/harness-engineering]], and its response is a harness
mechanism rather than a model change. LangChain's countermeasure was a loop-detection middleware (see
[[DefinedTerm/agent-middleware]]) that counts edits per file through tool-call hooks and, after a set
number of edits to the same file, adds context suggesting the agent reconsider its approach. The team
reports that this can help an agent recover, but that the model may still continue down the same path if
it believes it is correct. It presents the guardrail as a heuristic designed around today's perceived
model issues, likely to become unnecessary as models improve; its broader takeaway lists blind retries
among the bad patterns a harness designer should detect and fix in the short term.

## Related Terms

- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/agent-middleware]]
- [[DefinedTerm/verification-loop]]
