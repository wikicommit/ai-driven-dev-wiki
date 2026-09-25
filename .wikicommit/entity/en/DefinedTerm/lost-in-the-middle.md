---
title: "Lost in the Middle"
type: "schema:DefinedTerm"
lang: en
tags: [llm, context-window, context-engineering]
sources:
  - type: url
    url: 'https://toss.tech/article/52631'
    hash: sha256:8e01a448bd2676b5a47e3ed4d8360ee248c40091ecec973ede57f55edea8cba1
  - type: url
    url: 'https://helloworld.kurly.com/blog/vibe-coding-with-claude-code/'
    hash: sha256:ebce348758ea4336c22fe2c0c79c3120371a0d7c62e9c800a099fbcd0248ecb2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
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

[[BlogPosting/predictable-vibe-coding-strategy-with-claude-code]] applies the same name both to
a single long document handed over at once and, in its troubleshooting section, to rules set at the
start of a conversation being ignored after around ten turns. Its worked example is a thirty-page specification given to a coding agent in one prompt, where the first and
last few pages are reflected in the result while requirements in the pages between are partly missed.
That post traces the name to a paper on the phenomenon, likens the pattern to the serial position
effect in human memory — primacy and recency, with the middle neither rehearsed nor still in short-term
memory — and suggests, as a possibility rather than a finding, that models trained on human-written
data may have inherited that bias. It keeps the term separate from a working-memory limit, where rules
are dropped because there are many distinct items to track even when the instruction is short. The
remedies it proposes are procedural: split a request into small turns checked one at a time, list the
items to be handled as an explicit to-do list and work through it, and divide a large exploration
across subagents so each works in a small context.

## Related Terms

[[DefinedTerm/context-rot]], [[DefinedTerm/context-engineering]], [[DefinedTerm/agents-md]],
[[DefinedTerm/curse-of-instructions]]
