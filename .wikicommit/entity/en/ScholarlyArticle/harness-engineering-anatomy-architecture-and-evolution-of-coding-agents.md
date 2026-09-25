---
title: "Harness Engineering: Anatomy, Architecture, and Evolution of Coding Agents — A Source-Code Study of Eleven Systems"
type: "schema:ScholarlyArticle"
lang: en
tags: [harness-engineering, agent-architecture, coding-agents, survey]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.00006'
    hash: sha256:b2b6be03cc43e6f9b52518921f9545373563aec224327e1bb29a30beea7b7ce0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A source-code study of eleven production coding-agent harnesses and one meta-harness, pinned to July 2026 releases, that maps seven canonical harness subsystems, catalogs 29 recurring design patterns and 13 cross-cutting observations, and argues that in the first half of 2026 the coding harness turned from a tool into a platform."
  author: ["Paul Barbaste", "Tristan Darrigol", "Germain Vu", "Tom Wiltberger"]
  datePublished: "2026-07-15"
  keywords: ["harness engineering", "coding agents", "LLM agents", "agent architecture", "platformization", "tool use", "multi-agent systems", "MCP", "agent skills"]
---

This preprint, by authors affiliated with Wavestone AI Lab and Inclusive Brains, sets out to give
[[DefinedTerm/harness-engineering]] a reference grounded in production source code. It starts from the
definition "an agent is a model plus a harness", treating the [[DefinedTerm/agent-harness]] as everything
except the model — the runtime that couples a language model to the world through its loop, tools,
context, safety controls, orchestration and extension surfaces. The corpus is eleven systems pinned to
July 2026 releases: the four provider-native flagships ([[SoftwareApplication/claude-code]],
[[SoftwareApplication/openai-codex]], [[SoftwareApplication/gemini-cli]] and
[[SoftwareApplication/mistral-vibe-cli]]) and seven open-source systems
([[SoftwareApplication/openhands]], Aider, [[SoftwareApplication/mini-swe-agent]],
[[SoftwareApplication/hermes-agent]], Pi, [[SoftwareApplication/opencode]] and
[[SoftwareApplication/openclaw]]), with [[SoftwareApplication/omnigent]] analysed separately as a
[[DefinedTerm/meta-harness]]. The Claude Code analysis draws on a circulated source snapshot from March
2026 rather than an official release, which the authors call the weakest link on reproducibility.

The paper states that it does not benchmark or rank the systems; it describes how they are built. Each
system is dissected along seven subsystems — agent loop, LLM integration, tools and actions, memory and
context, safety and permissions, orchestration, and extensibility — each with the minimal and maximal
implementation observed in the corpus. Because eight of the systems had already been audited in an April
2026 edition of the study and were re-pinned rather than replaced, the paper also reports a quarter-long
longitudinal comparison of the same harnesses. It closes with 18 design recommendations and a roughly
90-line minimum-viable-harness scaffold in Python that the authors say implements ten of them directly.

## Key Points

- The seven subsystems are presented as the canonical anatomy of a harness, alongside two cross-cutting
  surfaces: an interface layer (TUI, CLI, IDE protocol, HTTP server, SDK) and a session substrate
  (transcripts, persistence, resume and fork).
- The paper distinguishes a harness from four things it is often confused with: a scaffold (a near-synonym
  it uses for the structural code, such as the loop and registries — see [[DefinedTerm/agent-scaffold]]),
  an agentic framework (a library imported to build an agent, as opposed to a runtime worked inside), an
  evaluation harness such as SWE-bench's (which wraps an agent rather than a model), and an orchestrator
  or meta-harness (which coordinates harnesses from above and implements no editing loop of its own).
- Across roughly four million lines of Python, TypeScript and Rust, the authors report that no agent
  runtime imports a general-purpose agentic framework such as LangChain, LangGraph or AutoGen, and that
  none retrieves code with vector embeddings; retrieval relies on ripgrep, tree-sitter, glob and
  auto-discovered Markdown context files. The authors describe this finding as structurally conservative:
  it rests on dependency manifests and import searches, not on tracing dynamic imports or internal forks.
- Skills in the SKILL.md format are reported in nine of the eleven systems and MCP in eight, so the paper
  concludes that skills now lead MCP in adoption; it attributes the change from an April tie to Pi, which
  implements skills while rejecting MCP.
- Seven of the eleven systems are reported to use threshold-triggered LLM compaction, and the paper argues
  that persistent memory, where designs diverge on who writes and who reviews the memory, has replaced
  compaction as the frontier of context management.
- OS-level sandboxing is described as among the most code-expensive capabilities in the corpus but as a
  choice rather than a consequence of scale: two of the largest systems, Hermes and OpenCode, ship no
  OS-level isolation primitives.
- The Agent Client Protocol is reported in six systems and to have acquired a third role — hosting whole
  harnesses, as when OpenHands runs Claude Code, Codex or Gemini CLI as interchangeable backends — while
  A2A remains, in the corpus, a Gemini CLI capability alone.
- The longitudinal comparison is described as showing convergence turning into imitation — Codex adopting
  Claude Code's hook event vocabulary verbatim and shipping an importer for its sessions and settings,
  OpenHands reading Claude Code's plugin format — and behavioural policy migrating from prompt prose to
  configuration. Three observations from the April edition were revised in place.
- The paper's thesis is that in the first half of 2026 the coding harness completed a turn from tool to
  platform: harnesses became importable SDKs while framework vendors shipped harnesses, marketplaces and
  governance layers appeared, and a meta-harness now orchestrates vendor harnesses behind one API.
- The authors propose a "scaffold–capability frontier" — a roughly concave relation between scaffold
  complexity and task success for a fixed model and task distribution — explicitly as a guiding intuition
  to be tested, not as a result.

## Notes

The authors list their own threats to validity: the analysis rests on reading source code rather than
runtime measurement, the qualitative scoring involves judgement calls, benchmark figures quoted are the
systems' own self-reported numbers on different models and dates, and the mapping between Anthropic's
published agent-design guidance and the observed architectures is described as suggestive rather than
causal. They also separate inventory claims such as tool counts and version pins, which they expect to
decay within weeks, from structural claims about loop taxonomy, subsystem anatomy and the absences, which
they expect to endure. The paper discloses that it was written with substantial assistance from
Anthropic's Claude via the Claude Code CLI, used both for the source-code analysis and for drafting, with
the findings verified against the referenced codebases.
