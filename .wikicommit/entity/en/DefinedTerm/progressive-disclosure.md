---
title: "progressive disclosure"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, context-engineering, terminology]
sources:
  - type: url
    url: 'https://github.com/agentskills/agentskills'
    hash: sha256:62d24fa3cf7cabfa0348af3065f32a15c43faf2d30b3352ff41f02e3a2399faa
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The term the Agent Skills specification uses for how agents load skills in three stages — holding only each skill's name and description up front and reading its full instructions into context only once a task matches."
---

Progressive disclosure is the term the Agent Skills specification uses for the way agents load skills: in three stages, rather than all at once. The specification states the consequence it is after directly — because full instructions load only when a task calls for them, agents can keep many skills on hand with only a small context footprint.

## Usage

The specification names three stages. At **discovery**, at startup, agents load only the name and description of each available skill, just enough to know when it might be relevant. At **activation**, when a task matches a skill's description, the agent reads the full `SKILL.md` instructions into context. At **execution**, the agent follows the instructions, optionally executing bundled code or loading referenced files as needed.

## Related Terms

The mechanism the specification describes this loading strategy for is [[DefinedTerm/agent-skills]].
