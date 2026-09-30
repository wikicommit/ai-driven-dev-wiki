---
title: "Review Loop Non-Convergence"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-code-review, agent-failure-modes]
sources:
  - type: url
    url: 'https://dev.to/quolu/how-i-fixed-the-infinite-feedback-loop-when-auditing-project-plans-with-claude-4gh'
    hash: sha256:4d822423c523e2709c1a8df03b98bad2af4a22e36ce6e3c9694e2e9de4c07ca3
  - type: url
    url: 'https://dev.to/zoetaka38/when-ai-reviews-ais-code-youve-built-an-infinite-loop-heres-how-we-stopped-it-4g1n'
    hash: sha256:e728a1e5ac20dcc643c605006d08b8675b906bc6c4143d31cd941d98c8d1418e
  - type: url
    url: 'https://tech-lab.sios.jp/archives/53091'
    hash: sha256:ad600fed8b9b62a03a62c07d1ed68806968ad524260b789712fdd5d404cb3432
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "The failure of a loop in which an AI reviews or audits work and the work is revised in response to settle: each revision draws new criticism, so the loop keeps going instead of reaching a state the reviewer accepts."
---

Review loop non-convergence is the failure of a review-and-revise loop — an AI auditing or reviewing a
piece of work, and the work being revised in response, often by an AI as well — to reach a stopping
point. Each revision is met by new criticism, often from a different angle than the last, so the loop
keeps producing work rather than settling. In
[[BlogPosting/how-i-fixed-the-infinite-feedback-loop-when-auditing-project-plans-with-claude]] the author
describes it for plan audits with Claude as "Whac-A-Mole" or a seesaw, with "no exit in sight";
[[BlogPosting/when-ai-reviews-ais-code-youve-built-an-infinite-loop]] describes the code-review form, in
which an AI reviewer's findings are handed to an AI fixer whose fix pull requests are reviewed in turn.

## Usage

The pattern in the plan-audit account is criticism that shifts direction from round to round: a part is
called weak from one perspective, then excessive once strengthened; an explanation is called redundant,
then insufficient once revised. The author reports that telling the model not to raise too many points,
or to stay consistent with its past feedback, did not help.

That post's explanation is about scope rather than prompting: as long as an audit's scope is broad,
points of criticism spring up without end, so no revision can exhaust them. Its remedy is to bound the
scope to something finite. For a plan that is already reasonably complete, the author restricted the
audit to logical contradictions only, and reports that the loop then converged after a few rounds,
reasoning that the number of contradictions in a plan is finite. This is one developer's account,
arrived at from personal use; the author mentions related ideas found afterwards — evaluation criteria
drifting during LLM-based review, and fixing the rubric before an evaluation starts — and says they
could not find existing work that clearly states the narrowing of the evaluation axis to a finite one.

The code-review account, from the builder of [[SoftwareApplication/orange-codens]], frames the problem as
one of termination and cost: an AI reviewer does not stop at "good enough" the way a human does, and every
round costs tokens, so it argues that termination has to be guaranteed by the architecture rather than
by the model. Its own non-convergence incident had the same shape as the plan-audit one — each review of a
bot's fix PR raised new high-severity findings on the newly written code, for four consecutive
request-changes rounds until an iteration cap escalated it. The fix it describes also bounds what the
review may ask for: on bot fix PRs, block only on unresolved serious findings carried over from the
previous review or on genuinely new blockers, and record other new findings without blocking. It sums
this up as "a perfectionist reviewer never converges". Alongside that, it lists structural cuts that keep
the fix cycle from restarting — handing off fixes only once a PR is merged, never handing off
automatically from bot-authored PRs, never dispatching a finding twice — and a second incident, in which
separate fix PRs for findings in the same file blocked one another until those findings were coalesced
into one task. This too is a single practitioner's account of their own system, not a measured result.

A third account, [[BlogPosting/splitting-one-greedy-ai-reviewer-into-three-agents-in-claude-code]],
gives the same shape for a document outline and puts numbers on it. Its author ran a review agent
built to score material from 0 and to find evidence of why it deserves 0 against a seminar outline,
fixed what it raised and resubmitted it, for three cycles; the outline grew from 685 to 772 lines while
its score fell from 47 to 44. Because that agent always finds evidence, each addition made in answer to
one finding became the target of new ones — "too dense", "reads like a disclaimer". Sorting the findings
into logical breakdowns and matters of taste, the author found the majority were taste. The remedy
again bounds what the review may raise: a separate reviewer that starts from 100, may report only five
named kinds of logical breakdown, and must report a clean result rather than look for defects when it
finds none — with the harsh reviewer kept for finished slides, and a person deciding which findings to
adopt. Like the other two, this is one practitioner's report of their own setup.

## Related Terms

- [[DefinedTerm/doom-loop]] — a single agent repeating variations of one broken approach, rather than reviewer and reviser failing to settle
- [[DefinedTerm/critical-dialogue-review]] — a two-model review loop whose described design caps its cycles and hands unresolved findings to a person
- [[DefinedTerm/review-finding-triage]] — judging each review finding before acting on it, rather than applying all of them
- [[DefinedTerm/closed-loop-ai-review]] — AI on both sides of a pull request
- [[DefinedTerm/llm-as-a-judge]]
- [[DefinedTerm/generate-review-revise-loop]]
