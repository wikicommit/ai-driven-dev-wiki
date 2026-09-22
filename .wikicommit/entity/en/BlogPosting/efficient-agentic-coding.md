---
title: "Effizientes Agentic Coding"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, code-review, testing, team-practices]
sources:
  - type: url
    url: 'https://www.production-ready.de/2026/09/07/agentic-coding-done-efficient.html'
    hash: sha256:b507ecb9845ab7dd33c04b325e8e71953a95bd8024012c732706d7c435df4c1a
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A consultant's summary of eighteen months of agentic coding in client projects and training, arguing that the gains come from letting an agent work unattended toward an explicitly described end state rather than treating it as a chat partner, and that the enabling conditions are explicit decisions, good test coverage and small reviewable changes."
  author: "David Ullrich"
  datePublished: "2026-09-07"
  publisher: "Production Ready"
---

Written eighteen months after Claude Code's release, this post gathers the author's experience of
[[DefinedTerm/agentic-coding]] in day-to-day project work and in client training. Its premise is
that outside the AI bubble many teams are still working out how to use these tools efficiently at
all, and that the author's conclusion from an earlier post — that coding is not the bottleneck —
has survived the intervening improvement in model capability.

The post's organizing distinction is that AI-assisted software development is not agentic coding.
An agent aims to work through a task autonomously; what makes the difference in practice, the
author argues, is not asking the model better questions but describing the desired end state
precisely enough that you do not have to be present while it is reached. Five sections then draw
out what that requires — not treating the agent as a pair-programming partner, making implicit
decisions explicit, feedback, review, and an accommodation with non-determinism — each closed with
a one-line "Learning".

## Key Points

- Agentic systems are described as consisting of the model plus a harness: the software environment
  that sends requests and receives responses, provides tools, and implements an agentic loop that
  iterates over a result, with guardrails and instruction files such as `AGENTS.md` or `CLAUDE.md`
  counted as part of the harness too.
- Treating a coding agent as a chatbot integrated into the IDE is argued to yield no large
  efficiency gain, because the constant back-and-forth keeps the developer's attention on the
  conversation; the gain comes from the agent working on its own while the developer does something
  else. The author's Learning for this section is not to babysit the AI.
- To get the expected result you must first be clear about what it is. The description is offered
  at several levels of abstraction: information about the system and the context the feature sits
  in, user personas and target audience, the precise feature definition from the user story,
  acceptance criteria, technical constraints, and even required class or method names.
- Dissatisfaction with an agent's output is attributed to missing context rather than to model
  capability, which the author says is good enough for most coding tasks.
- The central claim is that decisions a developer makes implicitly while implementing — where a
  class goes, what a method is called, how tests are structured — have to be made explicitly and in
  advance, because they are not obvious to a model that was never told them. Prompts running to
  several dozen lines are described as unremarkable, and the developer's job is recast as
  describing a task precisely enough not to be needed during it.
- Where those decisions belong is split three ways: some can be derived from the existing codebase
  by pointing the agent at a particular existing class, some hold for the whole project and belong
  in an `AGENTS.md` file, and anything specific to the current task belongs in the prompt or must
  otherwise be made reachable, such as access to the user story.
- Feedback means both correcting the agent in the next prompt and giving it something it can check
  itself against: static analysis, linters, and above all good test coverage, so that the code is
  semantically as well as syntactically correct. The author holds that end-to-end tests remain the
  most valuable kind and that an agent can produce good ones alongside the implementation that
  would have been too laborious to write by hand.
- On review, the author reframes the question as *when* a human reviews rather than *whether*: skip
  code review and the review happens on staging or in production by a product owner, and a defect
  found there means running the whole pipeline again. The familiar rule that the earlier a defect
  is found the cheaper it is to fix is asserted to hold unchanged under agentic coding.
- The difficulty of reviewing AI-generated code is attributed to how reviews are handled rather than
  to AI, which is said only to amplify it: large pull requests touching dozens of files along no
  clear line are simply not reviewable. The recommendations are to slice stories small, break them
  into implementable tasks, change one thing per pull request, review synchronously with
  colleagues, and review promptly and in batches rather than letting pull requests sit. A stated
  side benefit of synchronous review is that more people have read the code and project knowledge
  spreads.
- Non-determinism is presented as a feature of language models rather than a bug, controlled by
  temperature. The author's argument is that the development *process* was never deterministic
  either — different people, and the same person at different times, produce different solutions —
  and that the variation sometimes yields an approach the developer would not have thought of,
  while the generated code itself is deterministic once produced.

## Context

This is a practitioner's summary presented as such: the material is the author's own project
experience and client training over about eighteen months, with no measurements offered. Its
account of a harness — model, tools, agentic loop, guardrails and instruction files — is given in
the author's own voice, with the word itself linked out to writing elsewhere on harness
engineering; see [[DefinedTerm/agent-harness]] and [[DefinedTerm/harness-engineering]].

Much of the advice is deliberately continuous with pre-AI practice: small stories, small pull
requests, early defect detection and test-first development are presented as tools that still work
rather than as new findings, and the post's recurring move is to argue that agentic coding raises
the cost of doing them badly rather than changing what they are.
