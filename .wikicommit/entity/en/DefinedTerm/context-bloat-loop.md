---
title: "Context bloat loop"
type: "schema:DefinedTerm"
lang: en
tags: [context-window, spec-driven-development, agents]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62404/'
    hash: sha256:d49efd9233d456d1b205c748e19560ccabe3dc107352ab0e2e2f6f98094dd5ca
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An anti-pattern in agent-driven development in which a large spec and a complex workflow degrade an agent's behaviour, and each attempt to correct it by adding more context makes it worse."
---

A context bloat loop is an anti-pattern, named in [[BlogPosting/sdd-in-unity-client-antipatterns-and-improvements]], in which a large specification and a complex workflow lower the accuracy of an AI coding agent's behaviour, and attempts to correct that behaviour by piling on more context make it worse still. The post describes it as a negative loop: context that already fills most of the window triggers frequent [[DefinedTerm/compaction]], compaction makes the agent drop steps of its workflow, each dropped step is fixed by adding rules or memory, and the added context brings compaction back sooner.

## Usage

The post's example comes from an attempt at [[DefinedTerm/spec-driven-development]] on a Unity screen-transition library. Its single spec — `design.md` alone at 5,200 lines — took 73% of the standard context window before any work began, close to 90% counting the space reserved for auto-compaction, and project rules, CLAUDE.md and git operations added more. With compaction running often, the agent skipped test runs and declared tasks complete partway through; asking it to fix its workflow each time grew CLAUDE.md, memory and rules. The author reports lower implementation and test quality at the layers that combine classes, a lower rate of workflows completed without intervention, and a cap on parallel work.

The same post names two causes — the large single spec and over-extending the implementation workflow — and describes what broke the loop in a later project: splitting the work into smaller specs along technical boundaries, so that one spec set took about 17% of the window, and keeping resident context to a short set of primary rules while loading workflow detail on demand.

## Related Terms

- [[DefinedTerm/compaction]]
- [[DefinedTerm/context-rot]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/spec-driven-development]]
