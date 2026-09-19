---
title: "Code-Then-Execute Pattern"
type: "schema:DefinedTerm"
lang: en
tags: [security, prompt-injection, agent-architecture, agent-safety]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Jun/13/prompt-injection-design-patterns/'
    hash: sha256:bd74a0ffe03b1f53850aa0b16d091950d2f2544de525ebb6dade120e2b8ab4c4
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A design pattern for prompt-injection resistance in which a privileged model writes a program in a sandboxed domain-specific language that specifies which tools run and how their outputs flow between them, so that tainted data can be tracked through full data flow analysis."
---

The code-then-execute pattern has the privileged model emit a program rather than a sequence of
decisions. That program, written in a custom sandboxed domain-specific language, specifies which
tools should be called and how their outputs are passed to one another. Because the plan exists as
code before anything runs, the language can be designed to permit full data flow analysis — so that
data arriving from an untrusted source can be marked as tainted and tracked through the entire
process.

As summarized in [[BlogPosting/design-patterns-for-securing-llm-agents]], the post describes this
as an improved version of the [[DefinedTerm/dual-llm-pattern]], and attributes it to an earlier paper
that the reviewed paper includes among its six. Because that earlier paper is known here only
through this post's account of it, this page does not restate its own title, date or authorship.

## Usage

The pattern's distinguishing feature is the analysis the DSL makes possible. Where the dual LLM
pattern keeps untrusted content away from the privileged model by holding it in opaque variables,
this pattern additionally lets the system reason about where those values travel: which tool
consumes a tainted value, and what it is allowed to do with it. Enforcement therefore happens over a
program that can be inspected before execution, rather than over a running conversation.

## When It Applies

The pattern applies where the work can be expressed as a program over a fixed tool set, and where
someone is prepared to build and maintain the DSL and its analysis — it assumes both a custom
language and a sandbox to run it in, which is a substantially larger commitment than the other
patterns in the same group. It is misapplied where the tool set or the control flow cannot be pinned
down in advance. Its guarantees are bounded by the analysis: data flows the language cannot express,
or taints it does not model, are not covered.

It is one of six patterns presented together as trade-offs between an agent's utility and its
resistance to [[DefinedTerm/prompt-injection]], and the account available here is the reviewer's
rather than the paper's.

## Related Terms

- [[DefinedTerm/dual-llm-pattern]] — the pattern this one is described as an improvement on
- [[DefinedTerm/llm-map-reduce-pattern]] — another of the six, containing untrusted content in
  sub-agents rather than tracking it through typed data flow
- [[DefinedTerm/sandboxing]] — the isolation the generated program is executed within
- [[BlogPosting/design-patterns-for-securing-llm-agents]] — the source of this account
