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
  - type: url
    url: 'https://www.baccan.it/articoli/24-specdrivendevelopment-it'
    hash: sha256:5b0a7edc91981e6b533c582fa956710b666f767d417899b896125e2b99d98a3d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A requirements-engineering format that writes each requirement in one of a small set of fixed sentence shapes built from keywords such as WHEN, IF, WHILE, WHERE and SHALL, used in spec-driven development to leave an AI agent no room to interpret a requirement."
---

The Easy Approach to Requirements Syntax (EARS) is a format from requirements engineering that writes
each requirement in one of a small number of fixed sentence shapes, so that its trigger, its
condition and the system's obligation are stated explicitly rather than left to interpretation. A
practitioner's guide to spec-driven development gives five patterns, each ending in a
`THE SYSTEM SHALL` clause: **ubiquitous** requirements ("THE SYSTEM SHALL validate workspace permissions on every task operation"); **event-driven**
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

An Italian-language post by Matteo Baccan on spec-driven development makes a similar case. It presents
EARS as the option for anyone who wants to eliminate the ambiguities of natural language from a
specification: structures of the form "WHEN [event] THE system shall [action]" tie each decision to a
logical constraint that can be tested automatically. It notes that the syntax was not born for
artificial intelligence, and argues that a notation devised to prevent misunderstandings between
people has turned out to suit communication between developer and machine.

The two sources describe the format's origin differently. The practitioner's guide calls it a
30-year-old format from requirements engineering. Baccan's post says it was created by Alistair Mavin
at Rolls-Royce in 2009 for the requirements of aircraft engines.

## When It Applies

The practitioner's guide recommends it for writing the functional requirements of a specification, in
a workflow whose requirements phase produces a list of behaviours together with the acceptance criteria
that prove each one; in its worked example, the EARS-formatted requirements sit next to a list of
concrete acceptance examples the agent must satisfy. Baccan offers it as an optional step beyond a
plain Markdown specification rather than a requirement of the practice. The case for using it with AI
agents rests on these practitioners' recommendations — the guide's author calls it the
highest-leverage technique that almost no guide teaches — rather than on a measured comparison.
