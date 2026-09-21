---
title: "Testing Skyscraper"
type: "schema:DefinedTerm"
lang: en
tags: [testing, software-process, agents]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60882/'
    hash: sha256:7997cccac08ed6a2731d85a3012e81cea6de4b141192497c171f97de0740feb1
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A test strategy that drops the test pyramid's prescribed proportions and treats every layer as worth expanding — including integration and end-to-end tests — on the argument that under agent-driven development, where code changes fast, the pyramid's maintenance objection largely dissolves even though its execution-time objection does not."
---

The testing skyscraper is a test strategy that replaces the test pyramid's graded proportions with the position that tests at every layer are good and any layer may be written in quantity where it is useful. Where the pyramid allocates roughly 70–80% of tests to the unit layer, 15–25% to integration and 5–15% to end-to-end — on the grounds that the higher layers are slow to run and expensive to maintain — the skyscraper holds that all types are GOOD, and that writing many of any of them is acceptable.

## Usage

[[BlogPosting/redesigning-code-review-for-the-ai-era]] adopts the term for a team that reached it by asking whether the pyramid's reasoning still applies after adopting coding agents roughly doubled its commit count. That post's argument is that under agent-driven development code changes rapidly and package and dependency updates are frequent, so unit tests alone stop being sufficient assurance, and the question becomes whether the pyramid's cost objections still bind.

The post's answer is that one of them has largely dissolved and the other has not. Maintenance cost — historically the reason to keep the upper layers thin — is said to be mostly solved by the same agents that created the pressure: a guideline instructing the agent to update the tests whenever it changes the code means the agent generally does so unprompted. Execution time is not solved, and the post's remedy is scheduling rather than restraint: run only lightweight tests when a pull request is opened, and defer the heavy end-to-end suite until after review approval, using a merge queue, so that what reaches the main branch is still fully verified without developers waiting on it.

Its reported outcome, given for the backend team specifically, is a test-to-code line ratio that rose from 78.6% in June 2025 to 95.2% in September and 112.6% by December — more lines of test than of code — alongside full end-to-end and integration coverage of the APIs and batch jobs that end users touch, reached within six months of adopting coding agents.

## When It Applies

The strategy assumes two things that are not always present. The first is an agent-assisted workflow disciplined by written guidelines, since the whole maintenance argument rests on the agent reliably updating tests alongside code; without that, the pyramid's original objection returns intact. The second is infrastructure able to run tests selectively and at different moments — a merge queue or equivalent — because otherwise the execution-time cost the post concedes is unsolved lands directly on developer waiting time.

The post does not discuss how the strategy might be misapplied. What it does keep hold of is the pyramid's underlying reasoning about cost and speed: the maintenance and execution-time problems are addressed rather than dismissed, which is why the change it describes is to the proportions rather than to the reasoning behind them.

As for how well established it is: the term comes from an external article the post cites rather than from the team itself, and everything reported here is one team's adoption of it over six months in a single monorepo. The test-ratio figures are that team's own measurements; the claim that agent-maintained tests dissolve the maintenance objection is its experience, not a measured comparison against a team that did not do this.

## Related Terms

[[DefinedTerm/red-green-tdd]], [[DefinedTerm/test-design]], [[DefinedTerm/spec-driven-test-generation]], [[DefinedTerm/review-bottleneck]], [[DefinedTerm/data-aware-testing]]
