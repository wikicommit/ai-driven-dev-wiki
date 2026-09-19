---
title: "Writing about Agentic Engineering Patterns"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, coding-agents, technical-writing]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Feb/23/agentic-engineering-patterns/'
    hash: sha256:2e0749860bb2041b583e646cdfe9ae5c095aa1e10ca0a52b54ac9fbcf3fcb72b
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The post announcing Agentic Engineering Patterns, a chapter-shaped guide to working with coding agents. It fixes the terminology the project rests on, introduces a 'guide' format for evergreen writing on a blog, and states a policy against publishing AI-generated prose under the author's own name."
  author: ["Simon Willison"]
  datePublished: "2026-02-23"
---

This post announces [[CreativeWorkSeries/agentic-engineering-patterns]], a project to collect and
document coding practices for getting good results out of coding agents. Its stated goal is to answer
"how do I get good results out of this stuff" in one place, against a body of the author's own
existing writing on the subject that he characterises as relatively unstructured.

Before describing the project the post fixes its vocabulary. [[DefinedTerm/agentic-engineering]] is
used for building software with coding agents, with the defining feature named as the ability to both
generate *and* execute code, which lets the agent test and iterate independently of turn-by-turn
human guidance. [[DefinedTerm/vibe-coding]] is kept in what the post calls its original definition —
coding where you pay no attention to the code at all — and the two are placed at opposite ends of a
scale, with agentic engineering described as professional engineers amplifying existing expertise.

The remainder is about form rather than content. The post introduces a publishing format the author
calls a *guide*: a collection of chapters, where a chapter is a blog post with a less prominent date,
designed to be updated over time rather than frozen at first publication — his answer to the problem
of publishing evergreen material on a blog. It also states a personal policy of not publishing
AI-generated writing under his own name, which he says will hold for this project.

## Key Points
- Agentic Engineering Patterns is a new project collecting coding practices and patterns for getting
  the best results out of coding agents.
- "Agentic engineering" is used to mean building software using coding agents — tools whose defining
  feature is that they can both generate and execute code.
- That execution capability is what allows an agent to test its own code and iterate on it
  independently of turn-by-turn guidance from a human supervisor.
- "Vibe coding" is used in its original definition: coding where you pay no attention to the code at
  all, today often associated with non-programmers using LLMs to write code.
- Agentic engineering is placed at the opposite end of that scale — professional software engineers
  using coding agents to amplify existing expertise.
- The project is structured as a series of chapter-shaped patterns, which the author describes as
  loosely inspired by the format popularized by the software design-patterns literature.
- The author's existing writing under his `ai-assisted-programming` tag is described as extensive but
  unstructured, which is the gap the project is meant to fill.
- Two chapters were published alongside the announcement: one on writing code having become cheap,
  and one on red/green TDD helping agents write more reliable code with minimal extra prompting.
- The intended cadence is one to two chapters a week, with no planned stopping point.
- The author states a strong personal policy of not publishing AI-generated writing under his own
  name, and says it holds for this project; LLMs are used for proofreading, example code and side
  tasks, but not for the prose.
- A "guide" is introduced as a new content shape on the author's site: a collection of chapters, each
  a blog post with a less prominent date, designed to be updated over time rather than frozen.
- Guides and chapters are presented as the author's answer to publishing evergreen content on a blog,
  a problem he reports having been trying to solve for a while.
- The author reports that almost all of the implementation behind the new format was written by
  Claude Opus 4.6 running in Claude Code for web, accessed from his phone — his own account of how
  the code was produced.

## Context
The post is an announcement and a terminological statement rather than an argument, and its
definitions are offered as the author's own usage for the purposes of this project rather than as
consensus. It is also a partial demonstration of its own subject: the author reports having built the
site machinery for the new format with a coding agent while writing the prose himself, which lines up
with the split his definitions draw. The project's framing — that the field is moving fast enough to
need a structured place to put what works — is stated as motivation rather than defended.
