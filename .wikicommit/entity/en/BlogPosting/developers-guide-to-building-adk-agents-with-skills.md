---
title: "Developer’s Guide to Building ADK Agents with Skills"
type: "schema:BlogPosting"
lang: en
tags: [agent-skills, context-engineering, agent-tooling]
sources:
  - type: url
    url: 'https://developers.googleblog.com/developers-guide-to-building-adk-agents-with-skills/'
    hash: sha256:552a302bdbf41a13a25459078e2cb925659f4e0b64989d975a5df079730baa37
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Google for Developers guide to loading domain expertise into Agent Development Kit agents on demand through its SkillToolset, walking through four skill patterns that end in a skill factory, where a meta skill lets the agent write new skills at runtime."
  author: ["Lavi Nigam", "Shubham Saboo"]
  datePublished: "2026-04-01"
  publisher: "[[Organization/google]]"
---

This post is a tutorial on the `SkillToolset` of [[SoftwareApplication/agent-development-kit]] (ADK), which lets an agent load domain expertise on demand rather than carrying it in its system prompt. Its opening question is whether an agent that can follow instructions can also write new ones, and its answer is that with the right skill configuration an agent can generate entirely new expertise at runtime.

The problem it starts from is the monolithic prompt: developers often concatenate compliance rules, style guides, API references and troubleshooting procedures into one instruction string, which works for two or three capabilities but, at ten or more, costs thousands of tokens on every call whether or not the query needs them. The post presents the [[DefinedTerm/agent-skills]] specification's [[DefinedTerm/progressive-disclosure]] as the fix, and `SkillToolset` as ADK's implementation of it.

It then builds up four patterns, each extending the previous one, ending in a "skill factory" in which a [[DefinedTerm/meta-skill]] lets the agent expand its own capabilities by writing and loading new skill definitions.

## Key Points

- Progressive disclosure is described in three levels: L1 metadata (about 100 tokens per skill: name and description), loaded at startup for all skills as a menu; L2 instructions (under 5,000 tokens), loaded only when the agent activates a skill; and L3 resources such as style guides or API specs, loaded only when the instructions require them.
- The post's arithmetic is that an agent with 10 skills starts each call with roughly 1,000 tokens of L1 metadata instead of 10,000 in a monolithic prompt, which it calls roughly a 90% reduction in baseline context usage.
- `SkillToolset` auto-generates three tools that map onto the levels: `list_skills` (L1), `load_skill` (L2) and `load_skill_resource` (L3).
- Pattern 1, the inline skill, is a Python object with a name, description and instructions defined in agent code, recommended for small, stable rules that rarely change.
- Pattern 2, the file-based skill, is a directory with a `SKILL.md` and optional subdirectories for references, assets and scripts; any agent following the agentskills.io specification can load the same directory.
- Pattern 3, the external skill, is identical in code to Pattern 2 — the directory is simply downloaded from a community repository instead of written by hand.
- Pattern 4, the skill factory, is an inline skill whose instructions explain how to write valid `SKILL.md` files and whose L3 resources embed the specification itself and a working example; asked for a new capability, the agent generates a spec-compliant skill.
- Because a generated skill follows the same specification, the post states it works not only in ADK but in any compatible agent, naming Gemini CLI, Claude Code and Cursor among 40+ products that have adopted the format.
- The post recommends keeping a human in the loop to review generated `SKILL.md` files, treating them like a code review or a dependency, and testing any skill with evaluations before deployment.
- Its other tips: the `description` field is what the model sees at L1 to decide whether to load a skill, so it should say exactly when to activate; and skills should start inline and move to files only when they need reference documents or reuse across agents.

## Context

The post is a vendor tutorial from Google about its own framework; its figures for context savings are worked arithmetic from the stated per-level token budgets, not measurements. It points to the ADK skills documentation and a sample repository that runs all four patterns.
