---
title: "Easy Approach to Requirements Syntax"
type: "schema:DefinedTerm"
lang: en
aliases: ["EARS"]
tags: [spec-driven-development]
sources:
  - type: url
    url: 'https://felipefontoura.com/articles/what-is-spec-driven-development'
    hash: sha256:df2dca52352dcf718f101f98063eb1e945bc10156a4d147c303ee689675185ea
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A requirements-engineering format that writes each requirement in one of a small set of fixed sentence shapes built from keywords such as WHEN, IF, WHILE, WHERE and SHALL, used in spec-driven development to leave an AI agent no room to interpret a requirement."
---

The Easy Approach to Requirements Syntax (EARS) is a format from requirements engineering that writes
each requirement in one of a small number of fixed sentence shapes, so that its trigger, its
condition and the system's obligation are stated explicitly rather than left to interpretation. A
practitioner's guide to spec-driven development describes it as roughly thirty years old and gives
five patterns, each ending in a `THE SYSTEM SHALL` clause: **ubiquitous** requirements ("THE SYSTEM SHALL validate workspace permissions on every task operation"); **event-driven**
requirements introduced by `WHEN`; **state-driven** requirements introduced by `WHILE`;
**unwanted-behaviour** requirements introduced by `IF`; and **optional** requirements introduced by
`WHERE` ("WHERE notifications are enabled, THE SYSTEM SHALL notify assignees on change").

## Usage

In [[DefinedTerm/spec-driven-development]] it is used for the functional requirements of a
specification an AI agent will build from. [[BlogPosting/what-is-spec-driven-development-practitioners-guide]]
argues that the format suits that setting because it was built for exactly the ambiguity the practice
is fighting: its structure reads like a contract, and each shape leaves the agent no room to interpret.
The same guide's worked example writes the requirements of a payment-charge endpoint this way, each
numbered and paired with concrete acceptance examples — for instance, "WHEN the same Idempotency-Key is
replayed within 24h, THE SYSTEM SHALL return the original charge and create no new one", and "IF the
amount is <= 0, THE SYSTEM SHALL reject with 422 \"amount must be positive\"".

## When It Applies

The guide recommends it for writing the functional requirements of a specification, in a workflow
whose requirements phase produces a list of behaviours together with the acceptance criteria that
prove each one; in its worked example, the EARS-formatted requirements sit next to a list of concrete
acceptance examples the agent must satisfy. The case for using it with AI agents rests on this one
practitioner's recommendation — he calls it the highest-leverage technique that almost no guide
teaches — rather than on a measured comparison.
