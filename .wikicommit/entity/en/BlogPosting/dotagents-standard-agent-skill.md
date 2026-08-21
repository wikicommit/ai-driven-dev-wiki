---
title: "dotagents-standard: an Agent Skill for the AGENTS.md router pattern"
type: "schema:BlogPosting"
lang: en
tags: [agent-skills, context-engineering, agents-md, progressive-disclosure]
sources:
  - type: url
    url: 'https://www.jeffmixon.com/post/dotagents-standard-agent-skill/'
    hash: sha256:b41f531a8b968768046d0a7c12e5e9658ea9dd26d4b4f3ece81e2e7340854718
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Jeff Mixon's account of packaging the dotagents router/library convention as an Agent Skill, including the classification taxonomy that turns a bloated context file into a routed .agents/ directory."
  author: "Jeff Mixon"
  datePublished: "2026-07-08"
  publisher: ""
---

This post introduces `dotagents-standard`, an [[DefinedTerm/agent-skills|Agent Skill]] the author built to make an agent apply the [[DefinedTerm/dotagents]] convention on its own. It opens with the failure mode the convention exists to prevent: a project context file that starts small — a few build gotchas, a guardrail, a pointer to where the real content lives — and grows because each addition earned its place the day it was written. "The failure mode is cumulative": eventually the agent reads a database schema while editing CSS, a standing behavioural rule sits three paragraphs above a one-off decision from eight months ago, and nobody reads the file end to end before acting.

The author notes he had already been doing a version of this without naming it, splitting documentation three ways across some of his projects so an agent is not handed three audiences' content in one read — but applying it inconsistently, project by project. What was missing was a name for the general pattern and a way to make an agent apply it itself.

## Key Points

- **The classification step is the hard part, not the convention.** The post's stated observation is that reading the dotagents README is a five-minute exercise while applying it to an existing, messy context file is not, "the standard tells you *that* context should be split by kind, not *which kind a given paragraph is*." A seven-row taxonomy table maps each kind of content to its destination directory.
- **Two confusions are called out specifically.** *Rule versus memory*: a rule is a standing instruction you always obey, a memory is a fact or decision that explains history and may change — mixing them is called "the original sin the whole standard exists to prevent: you end up unable to tell 'you must' from 'we once decided.'" *Context versus specs*: context is durable and read-only across many tasks, while specs are what is being built right now and are superseded the moment the task ships.
- **The skill applies its own principle to itself** — the detail the author says he is proudest of. `SKILL.md` stays a screenful holding the mental model, the taxonomy table, two workflows (Utilize an existing setup, Implement a new one), and the router pattern; deeper material lives in a `references/` directory read only when the task needs that depth, with copy-paste templates and a fully filled-in example layout for a hypothetical billing API.
- **A good router rule names a trigger and carries an action verb.** The post's example rules pair a condition with `READ`, `CHECK`, `CONSULT` or `ADOPT`, so the agent knows what to *do* with a pointer rather than merely that a file exists. Its warning: "skip it, and an unconditional 'always read everything' router just recreates the monolith one directory deeper."
- **Memory is read/write.** When an agent makes a durable decision or learns a lasting preference mid-task, the instruction is to write it back so the next session inherits it instead of re-deriving it. And if a task needs context the router does not point to, that is treated as a bug in the router rather than a dead end — read the file, finish the task, then add the missing routing rule.
- **The stated argument for bothering** is that context bloat gets worse as agents take on more: more autonomy means more sessions, more accumulated decisions, and more temptation to append one more paragraph. "A single well-factored router pays for itself on the first session where the agent *doesn't* read a schema file to fix a stylesheet."

## Context

This is a practitioner's write-up of a tool he built, and the argument for the underlying convention is his own reasoning rather than measurement — no figures for context saved or quality gained are offered. He is careful to distinguish what he built from what he is building on: the convention is credited to its own author, and the post separates it explicitly from a broader protocol that shares the same directory name, on the grounds that "the two are easy to conflate."
