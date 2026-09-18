---
title: "Agent Command Environment (ACE)"
type: "schema:DefinedTerm"
lang: en
tags: [sase]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A proposed workbench for the human 'Agent Coach' in Structured Agentic Software Engineering (SASE) — a command center optimized for human cognition that supports specifying intent, orchestrating parallel agent work, and reviewing evidence-backed results."
---

The Agent Command Environment (ACE) is one of two purpose-built workbenches proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] as part of [[DefinedTerm/structured-agentic-software-engineering]] (SASE), alongside the [[DefinedTerm/agent-execution-environment]] (AEE) for agents. The ACE is the command center for the human "Agent Coach," a workbench optimized for human cognition rather than code-centric editing, offering full observability into agent activities and their associated costs.

## Usage

The paper describes the ACE as supporting both 1-to-N collaboration, where one developer works with many agents, and N-to-N collaboration, where a human team coordinates a shared fleet of AI teammates. It is where a coach authors and iterates on a [[DefinedTerm/briefingscript]], defines a [[DefinedTerm/loopscript]], and reviews structured evidence bundles such as a [[DefinedTerm/merge-readiness-pack]]; the environment also routes, presents, and records a [[DefinedTerm/consultation-request-pack]] when an agent needs to escalate a decision to a human specialist. The paper describes the ACE as needing capabilities missing from standard development tools today: disciplined N-version programming support (letting a developer visualize, compare, and mix components from multiple agent-generated solutions), program-comprehension views beyond simple textual diffs, strategic agent-team management (composing, evaluating, retraining, demoting, or retiring agents by capability and cost), and the ability for the coach to "jump in" to a traditional IDE view for a surgical code change before returning to the coaching workflow. It also proposes voice as a complementary interaction modality for high-level orchestration and mentorship tasks, citing evidence that speech can be faster than typing and that voice-assisted debugging can reduce context switching, and naming Talon Voice and Cursorless for VSCode as existing tools demonstrating the feasibility of speech-based agent interaction.

## Related Terms

[[DefinedTerm/agent-execution-environment]], [[DefinedTerm/structured-agentic-software-engineering]]
