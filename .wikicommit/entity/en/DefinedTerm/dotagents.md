---
title: "dotagents"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agents-md, progressive-disclosure, terminology]
sources:
  - type: url
    url: 'https://www.jeffmixon.com/post/dotagents-standard-agent-skill/'
    hash: sha256:b41f531a8b968768046d0a7c12e5e9658ea9dd26d4b4f3ece81e2e7340854718
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A convention for splitting a project's agent context into a slim always-read router at the repository root and a hidden library directory organised by kind of content, so an agent loads only what the current task matches."
  termCode: ""
  inDefinedTermSet: ""
---

dotagents is a proposal, credited to Brandon Greenwell, for splitting a project's agent context into a **router** and a **library**. The root [[DefinedTerm/agents-md]] file becomes the router: slim, always read, and responsible for telling the agent *where to look* for deeper context conditionally, rather than containing that context itself. A hidden `.agents/` directory holds the heavy material, organised by kind of content rather than by topic.

Its mechanism is [[DefinedTerm/progressive-disclosure]]: the agent loads a screenful of routing rules up front, then pulls in only the files the current task matches. The account here compares this to keeping a debug-only diagnostics endpoint out of production builds, or designing an API with one endpoint per concern rather than one that returns everything — "load what's needed, when it's needed, not before."

## Usage

**Seven kinds of content** each get their own subdirectory: `rules/` for standing behavioural constraints, `context/` for static reference material such as schemas or API types, `memory/` for durable decisions that evolve, `personas/` for specialised roles such as QA or architect, `skills/` for reusable multi-step procedures, `specs/` for the current task's requirements, and `logs/` for session records.

**Two distinctions carry most of the weight**, according to [[BlogPosting/dotagents-standard-agent-skill]]. A *rule* is a standing instruction you always obey; a *memory* is a fact or decision that explains history and may change — and conflating them is described as the original problem the convention exists to prevent, leaving a reader unable to tell "you must" from "we once decided." Separately, `context/` is durable and read-only across many tasks, while `specs/` is what is being built right now and is superseded the moment the task ships.

**Routing rules must be conditional to do any work.** The guidance is that each rule names a trigger and carries an action verb — `READ`, `CHECK`, `CONSULT`, `ADOPT`, `RUN` — so that the agent knows what to do with a pointer and, critically, *when*. An unconditional router that says to read everything simply recreates the monolith one directory deeper.

**`memory/` is read/write.** An agent that makes a durable decision or learns a lasting preference mid-task is instructed to write it back — an ADR appended to a decisions file, a preference noted in a user file — so the next session inherits it rather than re-deriving it. A task needing context the router does not yet point to is treated as a bug in the router: read the file anyway, finish the task, then add the missing rule.

**A broader `.agents` Protocol is a distinct superset.** It keeps the same directory idea but adds a global layer that merges with the project layer, machine-readable configuration files, structured sub-agents, tasks and memories with their own frontmatter schemas, and a public hub for sharing bundles. That post's stated guidance is to use core dotagents for hand-authored project context and reach for the Protocol extensions when a global layer or MCP wiring is needed — and to be explicit about which is meant, since the shared directory name makes them easy to conflate.

## Related Terms

dotagents is one concrete answer to the sizing problem [[DefinedTerm/agents-md]] documents, and its taxonomy overlaps with [[DefinedTerm/agentic-memory]] on the `memory/` axis and [[DefinedTerm/agent-skills]] on the `skills/` one. The tooling that applies it is [[SoftwareApplication/dotagents-standard-skill]].
