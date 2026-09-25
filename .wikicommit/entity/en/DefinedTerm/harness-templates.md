---
title: "Harness templates"
type: "schema:DefinedTerm"
lang: en
tags: [harness-engineering, coding-agents]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html'
    hash: sha256:cf7369071f56e7b3b36f7b003d612f4aa69fef17a7135ba19f2e22f2ad7e1cc6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A possible future evolution of service templates proposed by Birgitta Böckeler: a bundle of guides and sensors that ties a coding agent to the structure, conventions and tech stack of one of an organisation's common service topologies."
---

Harness templates are, in the proposal made in
[[BlogPosting/harness-engineering-for-coding-agent-users]], a bundle of
[[DefinedTerm/guides-and-sensors]] that "leash a coding agent to the structure, conventions and tech
stack of a topology". The article starts from the observation that most enterprises have a few common
service topologies — business services exposing data via APIs, event processing services, data
dashboards — covering most of what they need, and that mature engineering organisations often already
codify these in service templates. It suggests these might evolve into harness templates, and that
teams may start picking tech stacks and structures partly according to which harnesses are already
available for them.

## Usage

The article supports the idea with Ashby's Law of Requisite Variety, which it summarises as saying
that a regulator must have at least as much variety as the system it governs and can only regulate
what it has a model of. An LLM-based coding agent can produce almost anything; committing to a
topology narrows that space, making a comprehensive harness more achievable — "a variety-reduction
move".

## When It Applies

This is a speculative proposal, framed as something that "might" happen, not a reported practice. It
assumes an organisation already has a small set of recurring topologies. The author expects harness
templates to face the same problems as service templates — instantiated copies falling out of sync
with upstream improvements, and versioning and contribution difficulties — possibly worse, since
non-deterministic guides and sensors are harder to test.

## Related Terms

- [[DefinedTerm/guides-and-sensors]]
- [[DefinedTerm/harnessability]]
- [[DefinedTerm/harness-engineering]]
