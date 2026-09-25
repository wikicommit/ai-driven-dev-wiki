---
title: "Meta Skill"
type: "schema:DefinedTerm"
lang: en
tags: [agent-skills, agent-tooling]
sources:
  - type: url
    url: 'https://developers.googleblog.com/developers-guide-to-building-adk-agents-with-skills/'
    hash: sha256:552a302bdbf41a13a25459078e2cb925659f4e0b64989d975a5df079730baa37
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An agent skill whose purpose is to generate new skill definitions (SKILL.md files), so that an agent equipped with it can write and load new capabilities at runtime. Google's ADK guide calls the resulting pattern a skill factory."
---

A meta skill, as defined in [[BlogPosting/developers-guide-to-building-adk-agents-with-skills]], is a skill whose purpose is to generate new `SKILL.md` files. An agent equipped with one becomes self-extending: it can expand its own capabilities without human intervention by writing new skill definitions and loading them at runtime. The guide calls this arrangement "the skill factory", the fourth and last of its skill patterns for [[SoftwareApplication/agent-development-kit]].

## Usage

In the guide's implementation, the meta skill is itself an ordinary inline skill named `skill-creator`. Its instructions explain how to write a valid `SKILL.md` — kebab-case names of at most 64 characters, a description under 1,024 characters, step-by-step instructions, detailed domain knowledge moved into `references/`, and a `SKILL.md` kept under 500 lines. The key part is its resources: it embeds the [[DefinedTerm/agent-skills]] specification and a working example skill as L3 references, which the agent reads through [[DefinedTerm/progressive-disclosure]] when asked to create something new.

The guide's demonstrations are an agent asked for a Python security-review skill, which produces one covering input validation, authentication and cryptography with a severity-based reporting format, and a blog-writing agent that, lacking a skill for technical introductions, writes one on the spot. Because the output follows the same specification, the guide states that a generated skill can be saved and loaded in a later session and works in other compatible agents as well.

## When It Applies

The guide presents the meta skill as the end point of a progression — inline skills for small, stable rules, file-based and imported skills for knowledge that already exists — for the case where an agent needs a capability no existing skill provides. It assumes a skill format the agent can be taught from a written specification and a loader that can pick up the generated files.

Its stated risk is that a meta skill's output becomes the agent's behaviour. The guide therefore recommends keeping a human in the loop to review generated `SKILL.md` files before deploying them, treating them like dependencies under code review, and testing any skill's effectiveness with evaluations. The pattern is a recommendation from this single vendor guide, illustrated with demonstrations rather than measured results.

## Related Terms

- [[DefinedTerm/agent-skills]]
- [[DefinedTerm/progressive-disclosure]]
- [[DefinedTerm/tool-creation]]
