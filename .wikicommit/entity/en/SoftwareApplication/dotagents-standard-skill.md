---
title: "dotagents-standard"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-skills, context-engineering, progressive-disclosure]
sources:
  - type: url
    url: 'https://www.jeffmixon.com/post/dotagents-standard-agent-skill/'
    hash: sha256:b41f531a8b968768046d0a7c12e5e9658ea9dd26d4b4f3ece81e2e7340854718
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An Agent Skill that teaches an agent to apply the dotagents router/library convention — setting up a fresh .agents/ layout, migrating a bloated context file into one, or navigating an existing one without over-reading."
  applicationCategory: "DeveloperApplication"
  author: "Jeff Mixon"
  operatingSystem: ""
  softwareVersion: ""
  license: "MIT"
---

`dotagents-standard` is an [[DefinedTerm/agent-skills|Agent Skill]] packaging the [[DefinedTerm/dotagents]] convention so that an agent can apply it without being re-taught project by project. Its author's stated gap was that the convention itself is quick to read but hard to apply: the standard says context should be split by kind, not which kind a given paragraph belongs to, and that classification step is what the skill supplies.

## Overview

It triggers on three situations: setting up a fresh `.agents/` layout, migrating a bloated `AGENTS.md`, `CLAUDE.md` or `.cursorrules` into one, and working inside a repository that already has one while needing to navigate it without over-reading.

## Features

The skill applies [[DefinedTerm/progressive-disclosure]] to its own material. `SKILL.md` stays a screenful, holding the mental model, the classification taxonomy table, two workflows — *Utilize* an existing setup and *Implement* a new one — and the router pattern. Deeper material sits in a `references/` directory: one file goes subdirectory-by-subdirectory in depth, another covers the broader `.agents` Protocol superset, and both are read only when a task needs that depth. An `assets/templates/` directory holds copy-paste starters for a router file, a rules file, a decisions memory file, a persona and a skill; an `examples/sample-project/` directory holds a fully filled-in layout for a hypothetical billing API as the concrete counterpart to the blank templates.

Its guidance for router rules is that each names a trigger and carries an action verb — `READ`, `CHECK`, `CONSULT`, `ADOPT`, `RUN` — so a pointer tells the agent what to do and under what condition.

## History

Installation is `npx skills add zaventh/dotagents-standard-skill`, which the post says works for any agentskills.io-compatible agent and is kept current with the same CLI's check and update commands; for [[SoftwareApplication/claude-code]] specifically, a symlink into the user skills directory works as well. It is MIT-licensed, with CI validating the skill's own frontmatter and link-checking every reference on push — which its author frames as the artifact holding itself to the same bar it asks of other repositories.
