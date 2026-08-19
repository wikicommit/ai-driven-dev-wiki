---
title: "Building Effective AI Coding Agents for the Terminal: Scaffolding, Harness, Context Engineering, and Lessons Learned"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, context-engineering, developer-tooling]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05344'
    hash: sha256:29a5dfd46c7505affc599f6922ebba2f67d01e7f3a343df5347a42f435a08edc
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A technical report documenting the architecture and design rationale of OpenDev, an open-source terminal-native AI coding agent. It presents its scaffolding and harness architecture, context engineering subsystems, tool system, and five cross-cutting design tensions distilled into transferable lessons."
  author:
    - "Nghi D. Q. Bui"
  datePublished: "2026-03-13"
  keywords:
    - "AI coding agent"
    - "terminal-native agent"
    - "context engineering"
    - "agent harness"
    - "compound AI systems"
---

This technical report documents [[SoftwareApplication/opendev]], an open-source command-line coding agent, and the architectural decisions behind it. Its stated framing is a shift in the landscape of AI coding assistance away from complex IDE plugins toward versatile, terminal-native agents that operate directly where developers manage source control, execute builds, and deploy environments.

The author is explicit that the paper's purpose is not to present a novel algorithmic breakthrough, but to share the design decisions, trade-offs, and lessons learned from engineering a production-ready agentic coding system — bridging what he describes as a gap between closed-source industrial practice and open academic discourse. He positions it as, to the best of his knowledge, the first comprehensive technical report for an open-source, terminal-native, interactive coding agent, arguing that existing systems fall into one of two categories: benchmark-oriented frameworks with published papers but designed for automated evaluation rather than interactive daily use, and CLI-native agents that lack published technical reports documenting their design decisions.

Three engineering challenges organize the work: managing finite context windows over sessions that routinely exceed the model's token budget, preventing destructive operations when the agent can execute arbitrary shell commands, and extending capabilities without overwhelming the agent's prompt budget.

## Key Contributions

**Scaffolding and harness as separate phases.** The report frames the architectural response around two phases: [[DefinedTerm/agent-scaffolding]], which assembles the agent — system prompt, tool schemas, subagent registry — before the first prompt, and the [[DefinedTerm/agent-harness]], which orchestrates tool dispatch, context management, and safety enforcement at runtime.

**Per-workflow LLM binding in a compound AI system.** Rather than a single monolithic model, the system is described as a structured ensemble in which each cognitive workflow independently selects a model via user configuration. Five model roles are defined — action, thinking, critique, vision, and compaction — each with a fallback chain. The report argues this makes the system model-agnostic by construction, so that switching providers or optimizing cost requires only a configuration change.

**An extended ReAct execution loop.** The standard Reason-Act cycle is extended with an explicit thinking phase that runs without tool access and an optional self-critique phase. The report's stated rationale is that when tools are available, models tend to act quickly rather than think deeply — and that it is the absence of tool schemas from the API call, not an instruction to refrain from using them, that changes the model's behavior. The loop also includes doom-loop detection, which fingerprints each tool call as a hash of the tool name and arguments and escalates from an injected warning to an approval-based pause when the same fingerprint recurs.

**Context engineering as a first-class concern.** The report presents [[DefinedTerm/adaptive-context-compaction]], [[DefinedTerm/system-reminders]] to counteract attention decay, a dual-memory architecture separating an episodic summary from verbatim recent messages, per-tool-type result summarization with large-output offloading to scratch files, and an experience-driven memory pipeline that accumulates project-specific knowledge as a playbook of scored bullets.

**Token-efficient extensibility and defense-in-depth safety.** External tools are discovered lazily through keyword search over Model Context Protocol servers rather than having all schemas loaded upfront; the report states this reduced startup context cost from 40% to under 5%. Safety is enforced across five independent layers: prompt-level guardrails, schema-level tool gating through dual-agent separation, a runtime approval system with persistent permissions, tool-level validation, and user-defined lifecycle hooks.

## Notes

The report's discussion section distills five cross-cutting design tensions into lessons the author presents as transferable beyond this system: treat context as a budget rather than a buffer and design graduated reduction stages; inject behavioral reminders at the point of decision rather than upfront, using a user role rather than a system role and capping frequency per reminder type; make unsafe tools invisible rather than blocked, since a model cannot reason about capabilities it does not know exist; design tools to absorb LLM imprecision rather than demanding exact correctness; and bound every resource that grows with session length. A further lesson concerns measurement: the report argues that provider-reported token counts must be treated as ground truth, because providers inject invisible content that makes local token counting systematically underestimate actual usage.

The author is explicit about the report's main limitation: it documents architectural decisions and design rationale but lacks systematic quantitative evaluation, and names benchmarking against [[Dataset/swe-bench]] and terminal-interaction benchmarks as future work that would validate the architecture against established baselines.
