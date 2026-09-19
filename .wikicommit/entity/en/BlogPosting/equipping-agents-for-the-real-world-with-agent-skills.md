---
title: "Equipping agents for the real world with Agent Skills"
type: "schema:BlogPosting"
lang: en
tags: [agent-architecture, context-engineering, agent-tooling]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills'
    hash: sha256:e884d6fd1fe5becb8f432c99a20cf8b36e39d087e507037696b411e11d077ef5
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Anthropic's engineering post introducing Agent Skills — organized folders of instructions, scripts and resources an agent discovers and loads dynamically. It explains progressive disclosure as the format's core design principle, walks through the PDF skill as a worked example, and gives guidance for authoring and auditing skills."
  author: ["Barry Zhang", "Keith Lazuka", "Mahesh Murag"]
  datePublished: "2025-10-16"
  publisher: "[[Organization/anthropic]]"
---

This engineering post introduces [[DefinedTerm/agent-skills]] as the authors' answer to a problem they
frame as arising from capability rather than from any shortcoming: once general-purpose agents can
operate full computing environments, the open question becomes how to equip them with domain-specific
expertise in a way that is composable, scalable and portable. The post's proposed answer is deliberately
modest in form — organized folders of instructions, scripts and resources that an agent discovers and
loads on its own — and the authors argue that this simplicity is what makes it easier for
organizations, developers and end users to build customized agents and give them new capabilities.

The post's guiding analogy is that building a skill resembles assembling an onboarding guide for a new
hire: rather than building a separately engineered agent for each use case, anyone can specialize a
general agent by capturing procedural knowledge into a shareable package. The technical substance
behind that analogy is [[DefinedTerm/progressive-disclosure]], which the authors name as the core design
principle making the format flexible and scalable, and illustrate through the PDF skill that powers
Claude's document-editing abilities.

A note added to the post on December 18, 2025 records that Agent Skills has since been published as an
open standard for cross-platform portability.

## Key Points

- A skill is a directory containing a `SKILL.md` file whose YAML frontmatter carries two required
  fields, `name` and `description`; bundled instructions, scripts and resources are optional additions
  to that minimum.
- Progressive disclosure is presented as the format's core design principle, in three levels: every
  installed skill's `name` and `description` are pre-loaded into the system prompt at startup, the
  `SKILL.md` body is read only when the agent judges the skill relevant, and further bundled files are
  navigated only as needed.
- Because an agent with a filesystem and code execution need not read a skill in full, the authors
  state that the amount of context bundled into a skill is effectively unbounded.
- Skills may include code the agent runs as a tool at its discretion; the post argues this is warranted
  both on cost (sorting a list by token generation is far more expensive than running a sorting
  algorithm) and on determinism, since many applications require reliability only code provides. In the
  PDF skill's case a bundled Python script extracts form fields without either the script or the PDF
  entering context.
- The authoring guidance offered is to start from evaluation — identify capability gaps by running
  agents on representative tasks — and build skills incrementally against observed shortcomings, rather
  than anticipating what context the agent will need.
- The recommended response to a `SKILL.md` that has become unwieldy is to split its content into
  separate referenced files; where contexts are mutually exclusive or rarely used together, the post
  adds, keeping those paths separate reduces token usage.
- The authors single out a skill's `name` and `description` as deserving particular attention, because
  those are what the agent uses when deciding whether to trigger the skill at all.
- One recommended authoring loop is to have the agent itself capture its successful approaches and
  common mistakes into a skill, and to ask it to self-reflect when it goes off track — presented as a
  way to discover what context the agent actually needs.
- On security, the post states that a malicious skill may introduce vulnerabilities in the environment
  where it is used, or direct the agent to exfiltrate data and take unintended actions, and recommends
  installing skills only from trusted sources
  and auditing less-trusted ones before use, paying particular attention to code dependencies, bundled
  resources, and instructions that connect to untrusted external network sources.
- The authors state Skills were supported at publication across Claude.ai, [[SoftwareApplication/claude-code]],
  the [[SoftwareApplication/claude-agent-sdk]] and the Claude Developer Platform.

## Context

The post is the vendor's own account of a format it designed, and its claims about benefits are
accordingly the authors' own rather than independent findings; no evaluation or measurement is reported
in it. The one quantitative-sounding claim — that bundled context is "effectively unbounded" — is an
architectural argument about what a filesystem-backed agent need not read, not a measured result.

Two forward-looking positions are stated as intentions rather than as shipped behaviour. The authors say
they expect to explore how Skills can complement [[DefinedTerm/model-context-protocol]] servers by
teaching agents workflows involving external tools, and that they hope to enable agents to create, edit
and evaluate Skills on their own, codifying their own patterns of behaviour into reusable capabilities.

The post's security section is notable for arguing against its own format's frictionlessness: the same
property that makes a skill easy to share — that it is a folder of instructions and code the agent will
act on — is what makes an untrusted one dangerous, and the recommended response is manual audit rather
than any mechanism the format itself provides.
