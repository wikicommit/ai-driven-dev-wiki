---
title: "Lost in the Middle"
type: "schema:DefinedTerm"
lang: en
tags: [llm, context-window, context-engineering]
sources:
  - type: url
    url: 'https://toss.tech/article/52631'
    hash: sha256:8e01a448bd2676b5a47e3ed4d8360ee248c40091ecec973ede57f55edea8cba1
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The name for a language model making poor use of material sitting in the middle of a long input, while responding strongly to what is at the very beginning and the very end of it."
---

Lost in the Middle is the name given to a language model failing to make good use of content
positioned in the middle of a long input, while the beginning and the end of that input are the
positions it responds to most strongly. [[BlogPosting/making-ai-follow-team-rules]] uses the name
as one already in common circulation rather than as its own, glosses it as the phenomenon of a
model not using what sits in the middle when it is given a long input, and adds in passing that the
same situation is also spoken of as context pollution — an equivalence it asserts without
developing.

## Usage

The consequence that post draws out is positional rather than quantitative: material placed at the
front of a session does not stay at the front. As a coding agent accumulates file reads, generated
code and test output over the course of a session, instructions loaded at the start drift toward
the middle of the input, which is the position the model attends to least. The account given is
that by roughly the thirtieth iteration of the loop, the agent trusts the code and context it has
just read over the rules it read when the session opened, and that the front of the conversation
stops feeling like the front.

Read that way, the term describes a failure mode of *placement* rather than of instruction quality,
and it is used in that post as the reason a project-root instruction file such as `AGENTS.md` is
not sufficient on its own: the rule was supplied and was not wrong, it simply ended up where the
model would not use it. The remedy proposed there is not a better-written file but re-injecting the
relevant rules at points inside the agent loop — see [[SoftwareApplication/pfmls-stylepack]].

## Related Terms

[[DefinedTerm/context-rot]], [[DefinedTerm/context-engineering]], [[DefinedTerm/agents-md]],
[[DefinedTerm/curse-of-instructions]]
