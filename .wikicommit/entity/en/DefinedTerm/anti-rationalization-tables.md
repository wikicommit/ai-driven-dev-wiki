---
title: "Anti-Rationalization Tables"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agent-skills/'
    hash: sha256:b9423cb1290bb467c3a66aa51884a5717037c14bd668eeca8b09ca3fba6fa781
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A design choice in Addy Osmani's Agent Skills project: a table, embedded in each skill's instructions, of common excuses an agent (or a tired engineer) might use to skip a required workflow step, each paired with a written rebuttal."
---

Anti-rationalization tables are a design choice in Addy Osmani's [[SoftwareApplication/agent-skills]] project, described there as its most distinctive one: a table of common excuses an agent — or a tired engineer — might use to skip a required workflow step, each paired with a written rebuttal, embedded into a workflow's own instructions. Examples given for the practice include "This task is too simple to need a spec" (rebutted with: acceptance criteria still apply, five lines is fine, zero is not) and "I'll write tests later" (rebutted with: there is no later — write the failing test first).

## Usage

The technique is presented as a countermeasure to a specific failure mode: large language models are described as good at producing a plausible-sounding paragraph explaining why a particular task doesn't need a given step, so pre-writing the rebuttal to a rationalization removes the model's ability to talk itself out of the step in the moment. The same source argues the pattern works for human teams as well as agents, framing most engineering decay as people accepting plausible-sounding justifications for skipping work rather than deliberately choosing to do it badly.

## When It Applies

It applies wherever a workflow has a step that is easy to skip under time pressure and where the reasons for skipping it tend to repeat across instances — the source's own examples are about skipping specs, tests, and code review. It assumes the specific rationalizations worth pre-empting are already known from past experience, since the technique is presented as a team writing down the lies it has already told itself rather than a general-purpose template.

## Related Terms

[[SoftwareApplication/agent-skills]]
