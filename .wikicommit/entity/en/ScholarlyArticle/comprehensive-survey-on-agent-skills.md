---
title: "A Comprehensive Survey on Agent Skills: Taxonomy, Techniques, and Applications"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-skills, agent-architecture, survey]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.07358'
    hash: sha256:096f5ed37573599d6a6c7ead31f91dbe0c836695066c0ed2890efe4a97108983
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A survey from The Chinese University of Hong Kong, Shenzhen that treats agent skills — reusable procedural artifacts coordinating tools, memory and runtime context — as a foundational component of LLM agent ecosystems, and organizes the literature around a four-stage skill lifecycle."
  author: ["Yingli Zhou", "Shu Wang", "Yaodong Su", "Wenchuan Du", "Yixiang Fang", "Xuemin Lin"]
  datePublished: "2026-05-26"
  keywords: ["agent skills", "LLM-based agents", "skill acquisition", "skill retrieval", "skill evolution"]
---

This survey examines LLM-based agent systems through the lens of [[DefinedTerm/agent-skills]],
which the authors define as reusable procedural artifacts that coordinate tools, memory and runtime
context under task-specific constraints. Its starting argument is that access to tools — through
APIs, plugins and protocol layers such as the [[DefinedTerm/model-context-protocol]] — does not by
itself determine when a capability should be invoked, how several tools should be coordinated, how
failures should be handled or how outputs should be validated. The authors call this shortfall the
[[DefinedTerm/procedural-gap]] and present skills as what bridges it: the agent acts as the
high-level planner, while skills form the operational layer that turns abstract plans into reliable,
reusable and composable execution — the agent's "muscle memory", in the survey's phrase.

The survey formalizes a skill as a tuple of a root instruction document the agent can load and
follow, a set of auxiliary resources (reference documents, templates, executable scripts or domain
artifacts), and applicability conditions governing when the skill should be retrieved and applied.
It then organizes the literature around four lifecycle stages — representation, acquisition,
retrieval and selection, and evolution — reviews representative methods, platforms and application
scenarios within each, and closes with open challenges and research directions. The authors collect
the papers, data and projects they cover in a public repository, Awesome-Agent-Skills.

## Key Points

- Skills are distinguished from raw tools and MCP servers by encoding situated procedural knowledge —
  triggers, sequencing, fallbacks and pitfalls — as bounded, reusable artifacts; in the survey's words,
  tools expose operations while skills package know-how for using them in context.
- Skills need not be tool-centric: cognitive skills such as review checklists or analysis workflows
  mainly use the model's internal knowledge but still supply structure and reuse beyond ad-hoc
  prompting.
- For representation, the survey classifies skills by what their auxiliary resources contain:
  text-backed (references, examples, templates, rubrics), code-backed (scripts, helper functions,
  wrappers — bringing versioning, testing and dependency management into the skill lifecycle) and
  hybrid, where the coordination burden is highest.
- For acquisition, it distinguishes four families by the direct source of a skill: human-derived
  (expert authoring), experience-derived (distilled from an agent's own past runs), task-derived
  (constructed on demand for the current task, then validated) and corpus-derived (extracted from
  documentation, repositories and other external material). It treats them as complementary and
  judges experience-derived acquisition the most heavily studied.
- It describes experience-derived acquisition as a pipeline of four operations — selection,
  summarization and abstraction, memory organization, and procedural packaging.
- It separates skill retrieval (reducing a large skill pool to a candidate set, by dense, sparse,
  generative or structure-aware means) from skill selection (deciding which candidate to invoke and
  how to compose several), arguing that retrieving skills differs from document retrieval because
  invoking a skill can trigger tool calls, side effects and costs.
- It reports that selection research is moving from static relevance matching toward sequential,
  execution-aware decision making, and that selection must weigh cost and risk alongside relevance,
  since even curated skills can have negative utility on some tasks.
- It separates skill evolution from acquisition: evolution concerns how an already formed skill is
  revised, validated, coupled with the agent's policy, propagated through a shared repository and
  governed at runtime.
- Among its open challenges are weak trigger specifications (a useful procedure that is routed
  poorly), resource drift between a skill's main document and its attached scripts, admission quality
  as acquisition outpaces curation, and an asymmetry in which current systems are far better at adding
  skills than at safely rewriting or retiring them.
- Its proposed research directions include a unified skill schema with common fields for scope,
  triggering conditions, dependencies, versioning and safety constraints, and lifecycle-level
  robustness for skill libraries — drift detection, compatibility checks and versioned rollback.

## Notes

The survey reads the rise of dedicated skill platforms — it lists SkillNet, ClawHub, SkillHub,
SkillsMP and Skills.sh — as a sign that skills are increasingly managed as shared assets, and names
discoverability, provenance, contamination and ecosystem trust among the pressures that follow once
skills become shareable. Its application section spans software engineering, web
and GUI tasks, chatbots, robotics, finance, healthcare, games and social simulation.

It positions itself against two neighbouring literatures: work on tool use in LLM agents, and work on
retrieval-augmented generation and agent memory, which it describes as centring on retrieval and
memory state rather than on reusable procedural skills and their lifecycle.
