---
title: "Scion"
type: "schema:SoftwareApplication"
lang: en
tags: [monorepo, developer-infrastructure, agent-scale]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/redesigning-source-control'
    hash: sha256:6eef9526169f77948a21587667cdda2583e166d062e81b5b2f46bdc53c2be1ed
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "An in-house version control system built by Anthropic for its monorepo, designed around always-online agent and CI clients: a thin client fetches data from a horizontally scalable server that performs commits, merges and history queries and exposes them through an API."
  applicationCategory: "Version control system"
  author: "[[Organization/anthropic]]"
---

Scion is an in-house version control system that [[Organization/anthropic]] built to replace git for
its monorepo, described in [[BlogPosting/redesigning-source-control-at-anthropic]]. Anthropic says
it built Scion because a more than tenfold rise in merged changes, driven by Claude writing code,
had made source control its biggest development bottleneck, and that it fully migrated the monorepo
from git to Scion in five months with a team of seven people.

Its starting premise is that nearly all of the repository's clients are agents and jobs that are
always online. Where git gives every clone a complete, offline-capable copy of the repository, Scion
puts the work on a server that answers questions about history and blame, creates commits and
performs merges and rebases, while the client keeps only a bounded local cache, lays out working-copy
files and watches for filesystem changes.

## Capabilities

- **Changesets.** The unit of work is a changeset, an entry in a write-ahead log that records the files
  changed relative to its first parent, with content-addressed pointers to compressed file contents in
  blob storage. Changesets are created on the server, and refs are discouraged except for the main ref
  and release branches, so accepting changes needs no locking or cross-server coordination.
- **Derived data.** Blame, path history and commit-graph structures are computed from changesets
  through one generic mechanism, each defined recursively from a changeset's parents and computed
  either eagerly or on demand; new kinds can be added without changing the client.
- **API access.** Every source control query the client uses is also exposed as an API, so many CI
  jobs and tools — Anthropic names its automated bisect and revert pipelines — need no local
  repository at all, and many write workloads can skip the checkout.
- **Sparse and virtualized checkouts.** The client requests the trees and blobs it wants, starting
  from a root tree, rather than negotiating what it already has, so sparse checkouts and checkouts
  that materialize files on demand need no special support.
- **Tiered caching.** A per-node daemon serves objects to jobs on the node and talks to regional cache
  servers, which in turn ask the authoritative servers on a miss; all tiers answer the same calls, and
  Anthropic reports a cache hit rate above 99% at each tier.
- **Access control.** Scion supports access control on repositories and permissions on individual
  directories, so that sensitive code can be protected within the monorepo.

## Adoption & Ecosystem

Scion is used inside Anthropic only. The company reports its infrastructure footprint as 200 times
smaller in CPU and memory than the git mirroring setup it replaced, checkouts for CI and research
jobs about two orders of magnitude faster, and a 25% CPU capacity gain for CI; these are its own
measurements. It was built alongside Antique, Anthropic's code review tool, and draws on prior art
from Google's and Meta's large-monorepo source control systems.

Anthropic states that Scion is not a suitable replacement for git for general use: its ideas make
sense only for truly enormous monorepos, it diverges significantly from git, and it depends on
bespoke internal code review, code search and CI, so the company does not plan to offer it to other
organizations. It instead suggests that git servers could adopt some of Scion's ideas, such as
comprehensive server-side APIs, without departing from git's model.
