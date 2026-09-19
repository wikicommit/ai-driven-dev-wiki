---
title: "Design Patterns for Securing LLM Agents against Prompt Injections"
type: "schema:BlogPosting"
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
  description: "Simon Willison's 13 June 2025 review of a multi-institution paper proposing six design patterns that constrain what an LLM agent may do after it has read untrusted input. The post summarizes each pattern, endorses the paper's premise that general-purpose agents cannot currently offer reliable safety guarantees, and notes that one of the six is the author's own earlier proposal."
  author: ["Simon Willison"]
  datePublished: "2025-06-13"
---

This post reviews a paper on defending LLM agents against [[DefinedTerm/prompt-injection]], and is
the wiki's source for the six design patterns the paper proposes. Its author describes the paper as
an excellent addition to the literature on prompt injection and LLM security, and frames its value
as coming from what it declines to promise: rather than offering a general defence, it accepts a
trade-off in which agents are deliberately prevented from solving arbitrary tasks.

The post quotes the paper's own framing of that trade-off — that as long as both agents and their
defenses rely on the current class of language models, general-purpose agents are unlikely to
provide meaningful and reliable safety guarantees, which redirects the question to what kinds of
agents can be built today that produce useful work while resisting attack. The post calls this a
very realistic approach and says the willingness to limit agents' ability to perform arbitrary tasks
is an unpopular trade-off that gives the paper credibility.

## Key Points

- The organising principle the post highlights from the paper is that once an agent has ingested
  untrusted input, it must be constrained so that it is impossible for that input to trigger
  consequential actions.
- The post restates that principle in its author's own terms: any exposure to potentially malicious
  tokens entirely taints the output for that prompt, and an attacker who can insert tokens should be
  assumed to control both the text the model emits and any tool calls it can make.
- Six patterns are summarized — [[DefinedTerm/action-selector-pattern]],
  [[DefinedTerm/plan-then-execute-pattern]], [[DefinedTerm/llm-map-reduce-pattern]],
  [[DefinedTerm/dual-llm-pattern]], [[DefinedTerm/code-then-execute-pattern]] and
  [[DefinedTerm/context-minimization-pattern]].
- The author notes that one of the six is his own: he describes the dual LLM pattern as his own
  earlier proposal, says the paper describes his exact pattern, and reports that it is illustrated
  with a diagram. The post links that earlier write-up, which is not among this page's sources, so
  its date and title are not restated here.
- The post is explicit about one pattern it did not fully follow, saying it is slightly confused by
  context minimization before offering its own reading of it.
- The post reports that the paper closes with ten case studies, each with threat models and
  mitigations, and lists them; it singles out the SQL agent case study as a highly challenging
  environment to which the paper devotes three pages.
- From the software-engineering case study the post quotes a suggestion that a code agent interact
  with untrusted documentation only through a strictly formatted interface such as a formal API
  description, and it registers scepticism — wondering aloud whether a sufficiently creative
  attacker could still do damage within a thirty-character method name.
- The author states that he has been writing about prompt injection for nearly three years without
  the patience to produce a formal paper, and calls prompt injection the biggest challenge to
  responsibly deploying agentic systems.

## Context

The post positions this paper against an earlier one it had covered, which it describes as the first
it had seen to propose a credible solution to some of the challenges prompt injection poses for
tool-using LLM systems, and says the new paper includes that earlier proposal among its six. It also
reports that the earlier work was itself influenced by the dual LLM pattern. Because those other
documents are known here only through this post's account of them, this page does not restate their
own titles, dates or authorship as established facts.
