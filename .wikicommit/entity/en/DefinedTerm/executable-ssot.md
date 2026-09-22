---
title: "Executable SSOT"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, knowledge-management, claude-code]
sources:
  - type: url
    url: 'https://toss.tech/article/harness-for-team-productivity'
    hash: sha256:c578d09dce25f7293277154d1741cd800ad5d6afd7700ee897468e966f53f939
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A proposed name for team knowledge written as a plugin for a coding agent rather than as a document, on the argument that the same text serves as a guideline when a person reads it and as a system prompt when a model reads it, so that updating it changes how the team's agents behave immediately. The proposal is made around one particular agent's plugin and marketplace mechanism."
---

Executable SSOT is a term proposed in [[BlogPosting/raising-productivity-floor-with-harness]] for
team knowledge held as a coding-agent plugin instead of as a document. The argument behind the name
is that the same text has two readers: a person reads it as a working guideline and a manual, and a
model reads it as a system prompt carrying precise instructions. The author's claim is that this
makes the paradigm of document management shift from recording to executing — when the plugin code
is updated, the behaviour of the team's agents updates with it.

The starting complaint is about ordinary documentation. Wikis and note-taking tools are argued to
become stale information the moment they are written, because they exist for people to read; the
author presents plugin-defined knowledge as having a different character on that specific point.

## Usage

The term is used in that post as the reason to prefer a plugin marketplace over a knowledge base
for distributing how a team works, and it underpins the post's wider argument that the best
engineer's know-how should be packaged and distributed rather than left to individual aptitude —
see [[DefinedTerm/raising-the-floor]].

It is also what the post's proposed layering hangs on. Knowledge is to be split into a global layer
of company-wide rules such as security policy and baseline coding style, a domain layer holding a
team's or a business area's own logic, and a local layer of a repository's implementation detail,
on the analogy that a new joiner is not handed every company document at once. Layered that way,
the author argues, the accumulated plugins amount to a living knowledge base without a separate
retrieval system being built.

## When It Applies

The conditions the argument implicitly assumes are that the knowledge be expressible as text a
plugin can carry, and that the team already work through an agent that loads plugins — the post is written around one
particular agent's plugin and marketplace mechanism, and its examples are that agent's. Its
contrast case is retrieval-augmented generation, which the author argues is harder to foresee
because hybrid search and reranker scores determine what gets injected, whereas a plugin is
explicit text whose contents a developer can see and control.

How well established it is: this is one engineer's proposal in a single post, and the post itself
is unusually clear that it is offering a direction rather than a result — describing the whole
argument as hypothesis and possibility, and saying that whether plugin-based knowledge management
is actually effective is something that has to be tried. A commenter raises the objection that the
predictability advantage may not hold at scale, since tracking which of dozens of layered plugins
are active in a given task becomes its own visibility problem, and that a knowledge-retrieval tool
and a definition of behavioural rules are not really comparable in the first place.

## Related Terms

[[DefinedTerm/raising-the-floor]], [[DefinedTerm/claude-code-plugin-marketplace]],
[[DefinedTerm/software-3-0]], [[DefinedTerm/context-engineering]], [[DefinedTerm/agents-md]]
