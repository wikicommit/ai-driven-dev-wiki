---
title: "progressive disclosure"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, context-engineering, terminology]
sources:
  - type: url
    url: 'https://github.com/agentskills/agentskills'
    hash: sha256:62d24fa3cf7cabfa0348af3065f32a15c43faf2d30b3352ff41f02e3a2399faa
  - type: url
    url: 'https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills'
    hash: sha256:67f4d43862e0cdc95ff69a5da0f2ecb7b3ca20fb9db59e1962077b1c422289d1
  - type: url
    url: 'https://www.jeffmixon.com/post/dotagents-standard-agent-skill/'
    hash: sha256:b41f531a8b968768046d0a7c12e5e9658ea9dd26d4b4f3ece81e2e7340854718
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The term the Agent Skills specification uses for how agents load skills in three stages — holding only each skill's name and description up front and reading its full instructions into context only once a task matches."
---

Progressive disclosure is the term the Agent Skills specification uses for the way agents load skills: in three stages, rather than all at once. The specification states the consequence it is after directly — because full instructions load only when a task calls for them, agents can keep many skills on hand with only a small context footprint.

## Usage

The specification names three stages. At **discovery**, at startup, agents load only the name and description of each available skill, just enough to know when it might be relevant. At **activation**, when a task matches a skill's description, the agent reads the full `SKILL.md` instructions into context. At **execution**, the agent follows the instructions, optionally executing bundled code or loading referenced files as needed.

[[TechArticle/equipping-agents-for-the-real-world-with-agent-skills]], the post that introduced the mechanism, names progressive disclosure as "the core design principle that makes Agent Skills flexible and scalable" and divides it by *artifact* rather than by *stage*. On that account the **first level** is the `name` and `description` metadata, which the agent pre-loads into its system prompt for every installed skill at startup; the **second level** is the body of `SKILL.md`, read into context only if the agent judges the skill relevant to the current task; and the **third level and beyond** are additional files bundled in the skill directory and referenced by name from `SKILL.md`, which the agent navigates and discovers only as needed. The two framings describe the same loading behaviour — the specification's discovery, activation and execution stages line up with these levels — but the levels make the recursion explicit, since a referenced file may itself reference further files.

The post's analogy is a well-organized manual that starts with a table of contents, then specific chapters, and finally a detailed appendix. Its stated payoff is stronger than a footprint reduction: because an agent with a filesystem and code execution tools never needs to read a whole skill into context, "the amount of context that can be bundled into a skill is effectively unbounded."

### Applied to a repository's own context files

[[DefinedTerm/dotagents]] is progressive disclosure applied to project context rather than to skill or tool definitions: a screenful of routing rules is loaded up front, and only the specific files a task matches are pulled in afterwards. [[BlogPosting/dotagents-standard-agent-skill]] compares the principle to keeping a debug-only diagnostics endpoint out of production builds, or designing an API with one endpoint per concern instead of one that returns everything — "load what's needed, when it's needed, not before."

The same post supplies a neat demonstration of the principle applied reflexively: the skill that teaches the convention is itself structured that way, keeping its entry file to a screenful — mental model, taxonomy, two workflows, the router pattern — while depth material sits in reference files read only when a task requires it.

## Related Terms

The mechanism the specification describes this loading strategy for is [[DefinedTerm/agent-skills]].
