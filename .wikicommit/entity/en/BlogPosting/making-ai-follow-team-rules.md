---
title: "AI가 팀 규칙을 지키도록 하는 방법"
type: "schema:BlogPosting"
lang: en
tags: [coding-tools, context-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://toss.tech/article/52631'
    hash: sha256:8e01a448bd2676b5a47e3ed4d8360ee248c40091ecec973ede57f55edea8cba1
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A Toss Bank engineer's account of why team coding conventions written into a project-root instruction file stop being followed as an agent session lengthens, and of a plugin that instead injects the relevant rules through hooks at two points inside the agent loop."
  author: "김경윤"
  datePublished: "2026-09-08"
  publisher: "토스테크 (Toss Tech)"
---

This post, written by an ML engineer at Toss Bank, starts from a problem the author attributes to
how coding agents read code: an agent does not take in the overall context of a codebase, but only
the part it needs in order to make a change, and writes within that — so it does not hold to
conventions that operate at the scale of the whole project. The author contrasts this with how
human developers absorb conventions, by reading code others wrote and exchanging review comments
until, as the post puts it, time aligns everyone without anything being written down.

Two earlier attempts are described and rejected. Leaving the convention as a review comment makes
the team's agreements depend on whoever happens to remember them. Writing them into a project-root
instruction file — the post names `AGENTS.md` as the kind of file it means — fails differently: the
agent does read the file at the start of a session and does follow it early on, but stops as the
session lengthens. The author attributes this to [[DefinedTerm/lost-in-the-middle]], and adds a
second objection, that fine-grained rules are costly to put in such a file at all, since every
project pays for them in context whether or not they apply.

The post's own answer is to stop treating the front of the session as the only place team rules can
enter. Its reading of the agent loop is that one user request sets off dozens of tool calls, and
that the repeated portion of that loop had nothing injected into it. Borrowing the shape of the
older linter feedback loop — write code, run the linter, feed the errors back, fix, repeat — the
team put team conventions in the linter's slot, delivered through
[[DefinedTerm/agent-hooks]] by a plugin they call
[[SoftwareApplication/pfmls-stylepack]].

## Key Points

- An agent works from the local context of the change it is making, not from the codebase as a
  whole, so conventions that hold at the project level are the ones it fails to keep.
- Rules placed only at the start of a session are followed early and dropped later; the author
  attributes this to Lost in the Middle, describing the rules as ending up in the middle — the
  position the model attends to least — as the conversation grows.
- The problem is reframed as one of *when* and *how many* rules to surface, not *what* to tell the
  agent.
- The repeated part of the agent loop, where dozens of tool calls happen per request, is presented
  as the place team conventions were missing.
- The team's two injection points differ deliberately: immediately after a file is written (that
  file's body only, fast, at most two rules, meant to get the code fixed on the spot) and just
  before the agent finishes (the whole change as a `git diff`, slower, at most four rules,
  described as a last safety net).
- Rule selection is done with filename patterns and regular expressions rather than by calling a
  model, because the hook runs on every file write. The author reports that an AI-based relevance
  check added about ten seconds per request, and argues the hook only needs to narrow candidates
  since the agent makes the final call on relevance.
- Single-file hooks cannot see a defect that spans files — the post's example is a service class
  depending on a repository implementation rather than its interface, where each file is correct
  on its own — which is what the end-of-loop injection point exists to catch.
- A rule whose trigger is too loose is worse than no rule: the author reports one regex that
  matched Python f-string format specifiers as well as dictionary literals, firing in 21 sessions
  with zero resulting code changes, and argues that wrong feedback teaches the agent to disregard
  the rules. This figure is the team's own instrumentation of its own plugin.
- The author draws a line for what belongs in a rule at all: defects recognizable from the shape of
  the code become triggered rules, while defects that only appear at runtime — N+1 queries are the
  example — belong in always-loaded context instead, because the ways of expressing a loop keep
  growing.
- Distributing conventions by copying a template repository is rejected on the grounds that a
  template starts ageing the moment it is copied; the team instead keeps rules in one central
  repository that the plugin pulls in the background at session start.

## Context

The post sits alongside other writing that treats [[DefinedTerm/agent-hooks]] as the deterministic
counterweight to instructions a model may or may not follow, but applies the mechanism to a
different end: rather than allowing or blocking a tool call, the hooks here inject prose the agent
is free to act on or ignore, and the end-of-loop text says so explicitly, calling itself a reminder
to review rather than a hard failure.

The post is written throughout as one team's first-person account of the problem it hit and how it
solved it, and its supporting numbers are that team's own: the roughly ten-second overhead was
measured when an AI relevance check was briefly attached to the hook, and the 21 sessions with no
resulting code change come from the logging the team later added to the plugin itself. The post
does not say the plugin is available outside the company. One commenter raises the question of hit
rate directly, arguing that triggers as broad as the enum example would inject context too often to
be worth it.
