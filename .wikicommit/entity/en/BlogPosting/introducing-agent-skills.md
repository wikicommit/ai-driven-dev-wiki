---
title: "Introducing Agent Skills"
type: "schema:BlogPosting"
lang: en
tags: [agent-tooling, agent-architecture, context-engineering]
sources:
  - type: url
    url: 'https://www.anthropic.com/news/skills'
    hash: sha256:d9203771b21f47f29f2864693735d485c5abe5e9b35eed91551ec1cbcc4099c2
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Anthropic's product announcement for Agent Skills, covering what Skills are, the four properties claimed for them, and how they are made available across Claude apps, the Developer Platform API and Claude Code. Updated in December 2025 with organization-wide management, a partner directory and publication as an open standard."
  datePublished: "2025-10-16"
  publisher: "[[Organization/anthropic]]"
---

This is the product announcement for [[DefinedTerm/agent-skills]]. It points readers to the engineering
account in [[BlogPosting/equipping-agents-for-the-real-world-with-agent-skills]] for the design pattern,
architecture and development best practices, and confines itself to what shipped. Where that post explains why the format is shaped as it is, this one
states what shipped and where: Skills are described as folders of instructions, scripts and resources
that Claude loads when relevant, accessed only when they match the task at hand.

The announcement frames Skills by analogy to custom onboarding materials that package expertise, and
notes that users had already seen them at work: the file-creation behaviour in Claude
apps — spreadsheets, presentations — was already implemented as Skills before authoring your own became
possible.

A note added on December 18, 2025 records three subsequent additions: organization-wide management for
skills, a directory of partner-built skills, and publication of Agent Skills as an open standard for
cross-platform portability.

## Key Points

- Claude is described as scanning available skills while working, and on a match loading only the
  minimal information and files needed — the announcement's stated reason being to keep Claude fast while
  giving it access to specialized expertise.
- Four properties are claimed: skills are composable (they stack, with Claude identifying which are
  needed and coordinating them), portable (one format across Claude apps, Claude Code and the API),
  efficient (loading only what is needed, when needed), and powerful (able to include executable code for
  tasks where traditional programming is more reliable than token generation).
- In Claude apps, Skills are stated as available to Pro, Max, Team and Enterprise users, with
  Anthropic-provided skills for common tasks, customizable examples, and the ability to author custom
  ones; Team and Enterprise admins must enable Skills organization-wide first.
- Invocation in Claude apps is automatic rather than manual, and the announcement says skills appear in
  Claude's chain of thought as it works.
- A `skill-creator` skill is described as providing interactive guidance for authoring: Claude asks about
  the workflow, generates the folder structure, formats the `SKILL.md` file and bundles the resources,
  with no manual file editing required.
- On the Claude Developer Platform, Skills can be added to Messages API requests, and a `/v1/skills`
  endpoint gives programmatic control over custom skill versioning and management. Skills are stated to
  require the Code Execution Tool beta, described as providing the secure environment they need to run.
- Anthropic-created skills for the API are named as reading and generating Excel spreadsheets with
  formulas, PowerPoint presentations, Word documents and fillable PDFs; developers can create, view and
  upgrade skill versions through the Claude Console.
- In [[SoftwareApplication/claude-code]], skills are installed via plugins from the `anthropics/skills`
  marketplace or manually by adding them to `~/.claude/skills`, are loaded automatically when relevant,
  and can be shared with a team through version control. The
  [[SoftwareApplication/claude-agent-sdk]] is stated to provide the same Agent Skills support for
  building custom agents.
- The announcement states that the feature gives Claude access to execute code, and advises sticking to
  trusted sources for that reason.
- Stated forward work is simplified skill-creation workflows and enterprise-wide deployment capabilities
  for distributing skills across teams.

## Context

This is product communication rather than a technical or evaluative account: it states what is available
on which surface and what Anthropic claims for the format, and defers the design rationale to the
company's engineering post. Anthropic offers no measurements of its own for the efficiency or
capability claims.

The announcement is also the record of Skills moving from an internal implementation detail to a
user-authored format. Its own framing makes that transition explicit — the document-creation behaviour
users had seen was already Skills — which places the announcement at the point where an internal
mechanism became an interface other people build against.

Four customer statements from partner organizations are quoted in the announcement, describing intended
or early use in document generation, agent customization and finance workflows. Two of them do put
figures to the benefit — one claiming work that took a day now takes an hour, another saving hours of
effort — but these are the companies' own numbers, supplied as part of a launch, with no methodology
given for either.
