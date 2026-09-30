---
title: "AIレビューを6系統から1系統へ——「指摘ゼロ」で終われないループの切り方"
type: "schema:BlogPosting"
lang: en
tags: [agentic-code-review, claude-code, agent-failure-modes]
sources:
  - type: url
    url: 'https://zenn.dev/shimo4228/articles/review-chain-damping'
    hash: sha256:9b76db71bfd5c235019df5775fd519a7856f9c9844b26dcaf21b7527849a2814
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An August 2026 Japanese-language Zenn post in which a developer reports cutting a pre-commit AI review chain in Claude Code from six standing review lines to one (plus a conditional security review), after counting its results and concluding that its review-fix-re-review loop could not reach zero findings because it had no damping term."
  author: ["shimo4228"]
  datePublished: "2026-08-29"
---

In this Japanese-language post, a developer describes the pre-commit AI review setup of their personal
[[SoftwareApplication/claude-code]] environment — which they call a "review chain": several reviews run in turn
before a commit, findings are fixed, and the fixed diff is reviewed again — and why they cut it back. Each round
of fixes brought a new finding from the next review, and the loop never reached its implicit end condition of
zero findings. The author's conclusion is that the cause was structural rather than a matter of finding quality:
an LLM reviewer asked to look for gaps will usually return something even on sound work. So they cut the number
of review lines rather than trying to improve the findings.

## Key Points

- As of 22 August 2026 the author had six standing review lines — code simplification, code review for
  correctness, security review, detection of swallowed errors ("Silent-Failure"), a cross-check by a different
  model (OpenAI Codex), and a review for consistency with design records. Because some lines start several agents
  internally, a change could trigger around ten agents; the git history showed the additions concentrated in the
  ten days from 13 to 22 August, each a sincere improvement at the time.
- The author singles out replacing a home-made review agent with Claude Code's built-in `/code-review`, which
  starts multiple perspectives in parallel: one row in the table, but several times that row's bandwidth. Review
  bloat, they argue, grows not only by adding lines but by strengthening existing ones, which is harder to notice
  because the number of rows does not change.
- Counting the chain's results, the author found one demonstrated discovery: on 31 July a code review found a
  command-injection-class flaw common to seven hooks, confirmed reachable with a proof of concept. The dedicated
  security review had no demonstrated finding of the same level. Of six out-of-diff HIGH findings, only one — a
  blind spot that broke the review loop itself — was judged to have benefited from being handled immediately;
  two left unfiled were handled about a day later with no change in outcome, and the judgment for the other three
  was a counterfactual one.
- The author describes the loop as having no damping term, in control-engineering terms, and calls the resulting
  state oscillation. They cite Claude Code's official guidance as warning that a reviewer prompted to find gaps
  usually reports some even on sound work, and that chasing every finding leads to over-engineering.
- On 27 August the standing reviews were cut to one line — the built-in `/code-review`, run in a fresh context
  that sees only the diff — plus a security review that fires only for diffs touching trust boundaries.
  Simplify, Silent-Failure, the design-record review and the cross-model check left the standing set, the last
  becoming opt-in. Review effort was set explicitly to medium for all change types instead of high, since the
  author reads high as also reporting uncertain findings, which feed over-engineering. Out-of-diff findings are
  now filed only when they break the loop itself.
- A rule forbidding re-review after a fix was added and removed the same day: the author concluded that fixing
  and re-reviewing is a natural move of a sub-agent setup, and kept only the rule that a fix should be the
  smallest diff that answers the finding. Reviewers are told to report only gaps affecting correctness or stated
  requirements and to treat the rest as optional. A proposal to add monitoring for review bloat was rejected
  because it would itself be a new mechanism.
- The author presents "one standing line" as a local judgment based on their own counts, not an official
  recommendation, and lists the conditions under which they would reverse it — for example, oscillation
  recurring with one line, or the first real miss of a trust-boundary or swallowed-error defect.
- Readers running multi-stage AI review are advised to count three things before judging the findings: the
  number of standing review lines (including how many perspectives each runs), the effort setting of each, and
  the number of fix-and-re-review round trips.

## Context

The author states what is not yet known: that the number of review lines being the main cause of oscillation is a
judgment rather than a proof, that token savings are expected but not yet measured, and that there is no
before-and-after comparison of safety. They also describe the same self-feeding shape in another project of
theirs, a weekly unattended agent-repair pipeline whose own findings were mostly about the pipeline itself. The
post is one of several accounts collected under [[DefinedTerm/review-loop-non-convergence]].
