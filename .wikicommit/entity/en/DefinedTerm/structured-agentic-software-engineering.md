---
title: "Structured Agentic Software Engineering (SASE)"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A proposed engineering discipline for the Agentic Software Engineering (SE3.0) era that reimagines software engineering's four pillars — actors, processes, tools, and artifacts — around a duality between SE for Humans and SE for Agents, connected through dedicated workbenches and version-controlled artifacts."
---

Structured Agentic Software Engineering (SASE) is a vision proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] for making Agentic Software Engineering (SE3.0) structured, predictable, and trustworthy. It rests on a duality: the field must simultaneously serve SE for Humans (SE4H), which redefines the human's role toward high-level intent, strategy, and mentorship as an "Agent Coach," and SE for Agents (SE4A), which establishes a structured and predictable environment where multiple agents can operate effectively. Across this duality, SASE reimagines software engineering's four traditional pillars: actors expand from human developers to a hybrid team of human "Agent Coaches" and specialized agents; processes replace ad-hoc prompting with structured, repeatable engineering activities; artifacts become durable, machine-readable, version-controlled documents rather than transient prompts; and tools split into two purpose-built workbenches instead of one human-centric IDE.

## Usage

SASE is operationalized through two dedicated workbenches — the [[DefinedTerm/agent-command-environment]] (ACE) for the human coach and the [[DefinedTerm/agent-execution-environment]] (AEE) for agents — connected by a structured dialogue of version-controlled artifacts: humans initiate work with a [[DefinedTerm/briefingscript]], [[DefinedTerm/loopscript]], and [[DefinedTerm/mentorscript]], and agents respond with a [[DefinedTerm/consultation-request-pack]] or a [[DefinedTerm/merge-readiness-pack]], which humans in turn address with a [[DefinedTerm/version-controlled-resolution]]. Five named engineering activities operationalize this dialogue: [[DefinedTerm/briefing-engineering]], [[DefinedTerm/agentic-loop-engineering]], [[DefinedTerm/ai-teammate-mentorship-engineering]], [[DefinedTerm/agentic-guidance-engineering]], and the joint [[DefinedTerm/ai-teammate-lifecycle-engineering]]/[[DefinedTerm/ai-teammate-infrastructure-engineering]] discipline. The paper distinguishes this team-level, N-to-N collaboration among many humans and many agents from what it calls "agentic coding" — the current, largely 1-to-1 interaction between one developer and one AI assistant.

## When It Applies

The paper presents SASE as intentionally visionary rather than an implemented system: it is offered as a conceptual scaffold to catalyze community dialogue rather than a definitive solution, and its authors invite the community to challenge, refine, and extend the engineering activities it proposes. It argues SASE does not run counter to Richard Sutton's "Bitter Lesson" that general, compute-scaled methods outperform hand-baked structure, because that lesson is most potent where training data is abundant (e.g. building a common web application) and weaker for novel tasks or niche domains where a human is still needed to provide overarching structure. The paper's own worked example — a developer resolving seven pull requests by triggering agent teams to generate 28 candidate pull requests in parallel — illustrates the process and artifact gaps SASE is meant to address, rather than a deployed instance of SASE itself.

## Related Terms

[[DefinedTerm/agent-command-environment]], [[DefinedTerm/agent-execution-environment]], [[DefinedTerm/se-autonomy-levels]]
