---
title: "Deterministic quality gate"
type: "schema:DefinedTerm"
lang: en
tags: [agents, verification, software-process]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62404/'
    hash: sha256:d49efd9233d456d1b205c748e19560ccabe3dc107352ab0e2e2f6f98094dd5ca
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A quality check enforced by hooks or CI rather than left to an AI agent's instructions, so that a condition such as every test passing holds regardless of the agent's probabilistic behaviour."
---

A deterministic quality gate is a quality check enforced by the development environment — hooks, CI — rather than left to an AI coding agent's instructions, so that a condition such as every test passing holds regardless of how the agent behaves on a given run. [[BlogPosting/sdd-in-unity-client-antipatterns-and-improvements]] introduces it as the fix for tests being skipped in an agent-driven workflow, and locates the root cause of that problem in having entrusted quality assurance to an agent whose behaviour is probabilistic.

## Usage

In the post's first project, regression testing was a step in the agent's own workflow, and as the workflow grew more complex, whether tests actually ran became probabilistic: pull requests were merged with tests not passing, and reviewers had to find the inconsistencies. In the second project the test cases were settled together with humans at the design stage, and every one of them was run by a `SubagentStop` hook and by a GitHub Action before merge. The author reports that reviewers no longer needed to check pull requests or implementation logs to confirm tests had passed, which reduced review cost.

## When It Applies

The post applies it where an agent carries out a multi-step workflow that includes testing, and where the workflow is complex enough that the agent may skip steps. It assumes test cases are defined in advance — in the post, agreed with humans at design time — and that hook and CI infrastructure exists to run them. The practice is reported by one engineer from two infrastructure projects, not as a measured or widely established result; the post's own summary states it as a principle, that quality should be guaranteed deterministically by gates rather than left to an agent's probabilistic behaviour.

## Related Terms

- [[DefinedTerm/agent-hooks]]
- [[DefinedTerm/guardrails]]
- [[DefinedTerm/context-bloat-loop]]
