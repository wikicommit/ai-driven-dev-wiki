---
title: "Structured Agentic Software Engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, software-development-process, human-ai-collaboration, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A conceptual framework proposed by Hassan and colleagues for the agentic software engineering era, organized around a duality between SE for Humans and SE for Agents, two purpose-built workbenches, and a set of version-controlled artifacts that carry the human-agent exchange."
  termCode: "SASE"
---

Structured Agentic Software Engineering (SASE) is a conceptual framework proposed by Ahmed E. Hassan and colleagues in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] for making [[DefinedTerm/agentic-software-engineering]] structured, predictable, and trustworthy. Its core thesis is a *structured duality*: the field must simultaneously serve two symbiotic modalities — SE for Humans (SE4H), which redefines the human role around high-level intent, strategy, and mentorship as an "Agent Coach", and SE for Agents (SE4A), which establishes a structured, predictable environment in which multiple agents can operate effectively. The authors present it as a visionary conceptual scaffold intended to catalyze community dialogue, not as a validated methodology.

## Usage

SASE proposes that the duality requires rethinking four foundational pillars of software engineering, because each manifests differently across the two modalities:

| Pillar | Shift proposed by SASE |
| --- | --- |
| Actors | From human developers to a hybrid team of human "Agent Coaches" and specialized software agents |
| Processes | From ad-hoc prompting to structured, repeatable engineering activities governing human-agent collaboration |
| Artifacts | From transient, informal prompts to durable machine-readable artifacts serving as contracts and institutional memory |
| Tools | From the all-in-one human-centric IDE to specialized workbenches for humans and for agents |

On the tooling pillar, SASE proposes replacing the IDE with two environments: [[DefinedTerm/agent-command-environment]] for the human coach, and [[DefinedTerm/agent-execution-environment]] for the agents. The exchange between them is carried by explicit, version-controlled artifacts rather than an informal chat monologue — humans author a [[DefinedTerm/briefing-script]], a LoopScript, and a MentorScript; agents produce a [[DefinedTerm/consultation-request-pack]] and a [[DefinedTerm/merge-readiness-pack]]; and humans reply with Version Controlled Resolutions explicitly linked to the artifact they address.

The framework is operationalized through a set of named engineering activities rather than a single process: Briefing Engineering (BriefingEng), Agentic Loop Engineering (ALE), AI Teammate Mentorship Engineering (ATME), Agentic Guidance Engineering (AGE), and AI Teammate Lifecycle and Infrastructure Engineering (ATLE and ATIE). The paper presents this list as an initial scaffold rather than a definitive or exhaustive one, and invites the community to challenge and extend it.

A recurring emphasis is that SASE targets team-scale work rather than solo assistance. The authors distinguish *agentic coding* — the one-to-one interaction between a developer and an AI assistant, framed as an augmentation of a solo activity — from *agentic software engineering*, which must support N-to-N collaboration among many humans and many agents. SASE also acknowledges that SE is a "wicked problem" where rigid, universal processes are futile, and therefore argues that an AI teammate quickly onboarded into a specific team's context is more valuable than a brilliant but brittle specialist agent.

## Related Terms

SASE is one of several competing framings for [[DefinedTerm/agentic-software-engineering]]; its authors position it as building on Plan-Do-Assess-Review–style loops, Product Requirement Prompt–style briefs, and multi-agent frameworks such as BMAD, while differentiating itself through mentorship-as-code, the dual workbenches, merge-readiness as the target artifact, and consultability as a first-class artifact.
