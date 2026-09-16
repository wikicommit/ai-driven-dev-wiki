---
title: "Beads"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/code-agent-orchestra/'
    hash: sha256:f16aa303da51395585e293ea9d466a00847210974b774f822827f13f48b30431
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Gastown's persistent-memory pattern: immutable, git-backed records of every agent decision and outcome, with full provenance, queried through task graphs and a SQL-addressable data plane rather than vector-based retrieval."
---

Beads is a persistent-memory pattern from the Gastown project: immutable, git-backed records of every decision an agent makes and its outcome, carrying full provenance. Rather than storing this history as embeddings in a vector database, agents query past beads through task graphs and a SQL-addressable data plane, described as structured, queryable institutional memory that goes beyond what a flat markdown memory file can hold.

## Usage

It is presented as one of several techniques for making multi-agent development loops smarter over time, alongside per-agent token budgeting with kill criteria and self-reflection proposals written to a `REFLECTION.md` file after each task.

## Related Terms

[[DefinedTerm/ralph-loop]]
