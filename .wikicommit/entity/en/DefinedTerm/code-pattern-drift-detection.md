---
title: "Code Pattern Drift Detection"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, mcp, technical-debt]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/anchoring-to-reference.html'
    hash: sha256:b601ee397808d7ca15740ec6016dabb27ff69994f59a8f5677d5598aef271cb6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Using a coding agent to find where a codebase has drifted from the coding patterns of a reference application, such as a service template, and then to close those gaps — scoped by the reference application's own recent changes."
---

Code pattern drift detection is the use of a coding agent to compare a codebase with a reference
application — a compilable, runnable project that embodies an organisation's intended coding patterns,
such as a service template — and to identify where the codebase has drifted away from those patterns,
so that the gaps can then be closed. The term is used in
[[BlogPosting/anchoring-ai-to-a-reference-application]], which describes it as a second step after
using the reference application as the source of code samples a coding assistant works from.

## Usage

In the setup that article describes, a [[DefinedTerm/model-context-protocol]] server gives the agent
access both to the reference application's code samples and to its git commits. The prompt asks the
agent first to find the latest changes in the reference; the agent fetches the latest commit through
the MCP server, uses its diff to analyse the target application, and writes a drift report. A person
reviews and edits that report — removing irrelevant findings, for instance — and then, in a second step,
asks the agent to write code that closes the gaps it identifies. Scoping the comparison by the
reference's commits is how the user tells the agent what kind of drift to look for; the article reports
that asking the agent simply to compare the reference and target code instead produced many irrelevant
comparisons.

## When It Applies

The problem it addresses is that service templates, a typical building block of the "golden paths"
organisations build for their engineering teams, are meant to carry the current patterns and standards,
but once a service has been created from one, feeding later template updates back into it is tedious,
and generated code that is then extended and maintained often drifts from the reference. The approach
assumes such a reference application exists and is maintained, and that its changes are recorded as
commits an agent can read.

Where the drift is simple enough — adding a logger, changing a logging framework — deterministic codemod
tools such as OpenRewrite can close it, and the article advises considering them before reaching for
AI. It locates the agent's contribution in drift whose fix needs coding more dynamic than
regular-expression-based codemod recipes allow, such as turning varied, non-standardised log messages
into a structured format. How well-established the technique is: it is one practitioner's experiment,
tested on a deliberately simple example, with the author reporting that commit scoping had a good impact
rather than presenting any measurement.

## Related Terms

[[DefinedTerm/model-context-protocol]], [[BlogPosting/anchoring-ai-to-a-reference-application]]
