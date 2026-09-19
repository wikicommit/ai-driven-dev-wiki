---
title: "Writing code is cheap now"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-engineering, coding-agents, engineering-practice]
sources:
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/code-is-cheap/'
    hash: sha256:37ef48c7b1d1dbe1ac37ea7545119822fb55ed1169964387cd9bd4be4d57140c
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The premise, set out as a principle of agentic engineering, that coding agents have collapsed the cost of producing code while leaving the cost of producing *good* code largely intact — so that engineering habits built around code being expensive no longer hold, and new ones have to be developed deliberately."
---

"Writing code is cheap now" names the observation that coding agents have dramatically dropped the
cost of typing code into the computer, and the claim that getting comfortable with the consequences
of this is the biggest challenge in adopting agentic engineering practices. The argument is that
code has always been expensive — producing a few hundred lines of clean, tested code takes most
developers a full day or more — and that a great many engineering habits, at both the macro and the
micro level, were built around that single constraint.

At the macro level, the account runs, organizations spend considerable time designing, estimating
and planning so that expensive coding time is spent efficiently, and evaluate feature ideas by
whether the value they deliver justifies that time. At the micro level, developers make hundreds of
daily decisions on the same basis: whether a refactor is worth an extra hour, whether to write
documentation, whether an edge case deserves a test, whether a debug interface can be justified.
When the cost of producing code falls, those intuitions about which trade-offs make sense are
disrupted — and the ability to run parallel agents makes the calculation harder still, since one
engineer may be implementing, refactoring, testing and documenting in several places at once.

## Usage

The principle is paired with a deliberate qualification: delivering new code has dropped in price to
almost free, but delivering *good* code remains significantly more expensive. The source enumerates
what it means by good code — that it works; that we *know* it works, having taken steps to confirm
it to ourselves and others; that it solves the right problem; that it handles error cases gracefully
and predictably, with errors informative enough for future maintainers; that it is simple and
minimal, intelligible to humans and machines now and later; that it is protected by tests acting as
a regression suite; that it is documented at an appropriate level and that the documentation is
updated when behavior changes; that its design affords future change, balancing YAGNI against not
making future changes harder than they need to be; and that it meets the non-functional qualities
appropriate to the software — accessibility, testability, reliability, security, maintainability,
observability, scalability, usability.

Coding agent tools are said to help with most of this, while leaving a substantial burden on the
developer driving them to ensure the output is good for the subset of "good" the project actually
needs.

## When It Applies

The principle applies wherever agentic tooling has made code cheap to produce, and its practical
consequence is offered as a habit rather than a rule: whenever the instinct says "don't build that,
it's not worth the time", fire off a prompt anyway, in an asynchronous agent session where the worst
outcome is discovering ten minutes later that it was not worth the tokens.

It assumes an agent capable enough that the attempt is nearly free and a workflow in which a
discarded attempt costs little. Its stated limit is that the cheapness applies to production, not to
assurance — so treating cheap code as finished work is the misapplication the qualification above
guards against.

How well-established it is: the source presents this as a principle still being worked out. It
states that these best practices are still being figured out across the industry and that its author
is still figuring them out himself, and offers the "second guess yourself" habit as the best
available for now rather than as settled advice. It appears as a chapter in that author's own guide
to agentic engineering patterns.

## Related Terms

- [[DefinedTerm/agentic-engineering]] — the practice this is presented as a founding principle of
- [[DefinedTerm/verification-debt]] — the accumulation of unreviewed work that follows from
  production outpacing assurance
- [[DefinedTerm/review-bottleneck]] — where the remaining cost concentrates once writing is cheap
- [[DefinedTerm/the-70-percent-problem]] — a related account of where agent-produced code stops
  being nearly free
