---
title: "Redesigning source control at Anthropic"
type: "schema:BlogPosting"
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
  description: "An Anthropic engineering post describing how a more than tenfold rise in merged changes made git its biggest development bottleneck, and how a small team built Scion, an in-house server-centric version control system for always-online agent clients, and migrated the company's monorepo to it in five months."
  datePublished: "2026-10-13"
  publisher: "[[Organization/anthropic]]"
---

The post, written by [[Organization/anthropic]]'s source control team, starts from the claim that at
Anthropic coding is no longer the bottleneck: Claude can iterate on research loops, optimize programs
and build services at a speed and scale the company had not seen, and the constraint has moved to
developer infrastructure built for human scale — source control, builds and CI. It reports the company
going from around 2,500 code changes merged per day in May 2026 to over 30,000 per day by September,
and says it does not expect that growth to slow.

Its answer was [[SoftwareApplication/scion]], an in-house version control system, to which the
monorepo was fully migrated from git in five months, alongside a code review surface called Antique,
code search, a source control access-control system and other tooling built in the same period. The
post frames the project as a case study in which Claude's ability to write code both created the
problem and made it possible to build a scalable system to deal with it.

The argument for leaving git is about fit rather than fault. Git's decentralized design, in which
every clone is a complete repository that works offline, is described as right for the vast majority
of repositories, but Anthropic was using git as a centralized system with one authoritative copy while
nearly all of its clients were agents and jobs that are online by definition. The post asks what source
control would look like if designed from the start around agents being always online, and its
conclusion addresses the wider ecosystem: Scion is not offered as a git replacement, but some of its
ideas could be applied to git servers.

## Key Points
- At Anthropic, the post says, the bottleneck has moved from writing code to infrastructure built for
  human scale: source control, builds and CI.
- The monorepo's main-branch history is described as almost 100 GB, with on the order of 25 million
  checkouts per day for CI alone; the company had run several hundred internal git mirrors at its peak,
  which became harder to operate as the merge rate rose.
- Scion is built on stated principles: clients are always online; the server does the heavy work while
  the client holds little data; every source control query is available via API; every component
  scales horizontally; commits are cheap, incremental and lock-free; and the working copy is optional
  and sparse by design.
- The post reports Scion's infrastructure footprint as 200 times smaller in CPU and memory than the
  previous git mirroring setup, checkouts about two orders of magnitude faster, and a 25% CPU capacity
  gain for CI.
- A team of seven built Scion, Antique and about half a dozen related systems and completed the
  migration in five months, which the post contrasts with the years and larger teams such a system
  would previously have required.
- The engineers on the project would now rate Claude as better than themselves at writing code, yet
  supplied the system-level understanding and design trade-offs; the post says their role was often to
  tell Claude "no" when it violated core system constraints, and that adversarial review could be
  myopic and push Claude toward over-engineering.
- Reviewers still review every change request for the system, but examine the intent of a change
  rather than reading every line.
- Slack channels in which Claude is tasked with obsessively watching the health of one component —
  which the team calls "superfans" — are reported to catch subtle issues that traditional alerts miss.
- The team gave up on a merge queue with a global repository lock and invested instead in post-merge
  and pre-deploy automated testing, accepting that concurrent changes can conflict because Claude can
  usually fix the conflicts quickly.
- An early model snapshot asked to rewrite a handwritten prototype of the git-to-Scion ingestion
  pipeline is reported to have produced a version using 20 times less memory and running 4 times
  faster.

## Context
The post is explicit about its limits. Scion is said to make sense only for truly enormous
monorepos — with tens of thousands of engineers or swarms of agents writing code — and Anthropic is
described as unusual in how much it can spend on tokens internally. Because Scion diverges
significantly from git and needs its own code review, code search and CI, the company does not plan
to offer it in a broadly usable form. Instead it expects this class of problem to become common over
the next six to twelve months and suggests that git platforms could provide comprehensive server-side
APIs, a different negotiation protocol and better-composing sparse and shallow features without
abandoning git's model. It acknowledges prior art in large-monorepo source control at Google and Meta.
All performance figures are the company's own measurements of its own systems.
