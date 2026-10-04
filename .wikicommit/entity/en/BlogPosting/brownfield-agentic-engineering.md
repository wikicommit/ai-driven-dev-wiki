---
title: "Brownfield Agentic Engineering"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, legacy-code, verification, harness-engineering]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/brownfield-agentic-engineering/'
    hash: sha256:9e908973327fcd790eb88436c8412c9fc0a9343a93e8ec27945dd2416438a811
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "Addy Osmani's guide to using coding agents on long-lived brownfield codebases, where the repository no longer fully describes how the system behaves: zone the code by risk, write down only what the code cannot say, lock today's behaviour with characterization tests, migrate in complete units, and parallelize only once one unit has a dependable judge."
  author: "Addy Osmani"
  datePublished: "2026-09-14"
---

This post addresses [[DefinedTerm/agentic-engineering]] in brownfield systems — codebases that have been around long enough that "the repository is no longer a complete description of how the thing actually behaves," because institutional knowledge, legacy services and other teams' expectations live outside the tree. The author's summary of the problem is that agentic engineering in an old codebase "is about making hidden constraints visible and cheap changes trustworthy." Turned loose unsupervised on such a codebase, he warns, agents may produce something that "works" but with the wrong system design and brittle tests.

The post assumes the code should be the source of truth, with anything added on top limited to what cannot easily be inferred from it, and organizes its advice around zones, blast radius and a handful of patterns. Its closing claim is that agents "put a visible price on ambiguity": tribal conventions turn into recurring review comments, making countable a maintenance cost that was always paid during onboarding, review and incident recovery.

## Key Points

- Zone the codebase before an agent touches it: green for well-tested, current, isolated code where agents can iterate in a tight loop; yellow for mixed quality, where agents change code only after characterization tests exist; red for sensitive areas such as authentication, billing, permissions and payroll, where a human pairs on every step or the work does not happen.
- Three rules turn the zones into a procedure: a person draws the map, not the agent; zones move only when earned (yellow becomes green once characterization tests exist and the module's owner has reviewed the agent's first changes); and the zone sets the verbs.
- "Autonomy should follow blast radius, observability, and recoverability. A model's confidence is a poor guide."
- "Write down what the code can't say, and nothing else": agents infer a great deal from the repository, so written guidance should be reserved for business or team nuance, the trade-offs behind the structure, guidelines no tool enforces, domain rules, external constraints, and the history behind counter-intuitive code.
- For yellow and red work the author favours a separate read-only research pass that produces a short comprehension memo — entry points, owners, callers, existing abstractions, tests, production signals, history and open questions, each claim citing a file, issue, ownership record or dashboard — so the next agent does not repeat the same archaeology. Planning then starts from a clean context with a human choosing the path, implementation stops if the map proves wrong, and review starts fresh from the acceptance criteria.
- "Every repeated correction is a missing piece of the harness": a review comment that recurs should become a lint rule, hook, type, test or skill, with prose kept for constraints that cannot be enforced mechanically, so that over time the [[DefinedTerm/agent-harness]] becomes "a record of failures the team has decided not to pay for twice."
- Start with zero-risk work — explaining how the code works, then pinning today's behaviour with [[DefinedTerm/characterization-test]]s, ugly parts included, before mechanical transforms and dead-code inventories, and only later the hairiest parts. The same session should not both write the tests and make them pass.
- Where a surface has no honest unit suite, run the old and new paths side by side and promote only when their outputs match; the author cites GitHub's Scientist library and Netflix's GraphQL cutover as examples of this approach.
- Migrate in complete units: a migration is complete when the new path works and the old dependency is demonstrably gone, because half-finished migrations leave agents facing contradictory precedent. He warns that tests can stay green while a replacement still calls the legacy implementation, and that if deletion of the old path is left to a future cleanup ticket, the migration unit is not complete.
- From larger migrations he draws the lesson that "what transfers between companies is the structure around the agents" — porting guides written before any agent runs, a pre-existing test suite as the merge gate, and humans reviewing every change — rather than the headline numbers.
- Agents have changed the price of trying several plausible implementations, not the evidence required to choose one; the author reports CTOs letting teams have agents attempt multiple rewrites in different languages or frameworks to evaluate the trade-offs, and suggests having agents implement competing options that can all be checked against unit tests and performance-profiled before a decision is made.
- "Parallelize last": copy a factory's parallelism only after one unit has a dependable judge, a recovery path and a review format people can absorb, since parallelism multiplies whatever bottleneck already exists. He also notes that worktrees isolate changes but not behaviour, and that unattended agents consuming untrusted content need stronger sandboxes and scoped credentials.
- Lines generated say nothing about whether a codebase improved; he would track lead time, review minutes, human interventions, escaped defects, rollbacks, oracle mismatches and suppressions left behind, and for a migration the old imports remaining, traffic on the new path, parity mismatches and legacy dependencies removed.

## Context

The author draws on his own experience of long-lived codebases, including being called in on a day off to fix a broken AOL.com homepage whose many components were owned by dozens of departments, where changes without unit tests had to be user-tested by hand. He concludes that agents "don't remove the dozens-of-departments problem; they make it cheaper to attempt a change against it."

The migration examples he collects — Bun's Zig-to-Rust port, a controlled VB6-to-C# study, Stripe's TypeScript migration, Spotify's agent pull requests and Asana's test-library migration — are reported from other parties' accounts, and he flags limits on some of them, such as treating Asana's figure as a vendor-reported cost of generation rather than a controlled savings study. The post's "parallelize last" advice responds to [[DefinedTerm/software-factory]] patterns, and it lists three other posts by the same author as related reading: [[BlogPosting/agentic-skill-decay]], [[BlogPosting/audit-your-agent-files]] and [[BlogPosting/human-judgment-doesnt-leave-the-software-factory]].
