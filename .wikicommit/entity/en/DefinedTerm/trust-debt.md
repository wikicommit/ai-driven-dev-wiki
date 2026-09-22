---
title: "Trust Debt"
type: "schema:DefinedTerm"
lang: en
tags: [vibe-coding, code-review]
sources:
  - type: url
    url: 'https://tonybai.com/2026/02/28/agentic-software-engineering/'
    hash: sha256:71f1a7a4e0110bdb853371fac1dec6fd860c60643931805915db71acb1c96375
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A liability said to accumulate when agent-generated code is shipped faster than anyone can establish that it should be trusted. Introduced as the cost side of vibe coding's speed: the gain is real, and so is the debt building behind it."
---

Trust debt is the name [[BlogPosting/stop-vibe-coding-embrace-new-software-engineering]] gives to what accumulates when the speed of agent-generated code outruns the capacity to establish that the code deserves to be trusted. It is introduced as the other half of a trade rather than as a separate failure: the post grants that [[DefinedTerm/vibe-coding]] genuinely delivers speed, and places the debt directly against it — the speed is there, and trust debt is piling up wildly.

## Usage

The term is used to distinguish contexts rather than to condemn a technique. For a one-off script or a prototype, the post treats working by feel as fine and even magical; the debt is what makes the same approach untenable for long-lived software that has to be reliable, which it likens to designing a sea-crossing bridge in a paint program.

The account of how the debt accrues is about where the constraint sits. While humans typed code line by line, the physical limit on output incidentally bought time to absorb context, consider architectural boundaries and run a background quality check. Once generation stops being the bottleneck, human attention and review bandwidth become the binding constraint — the [[DefinedTerm/review-bottleneck]] this wiki names elsewhere, and the conventional response — open a pull request, read the diff — stops working against hundreds of lines produced in seconds across several microservices, with schema changes and new dependencies among them. What is left, in the post's characterization, is code that is locally over-optimized and globally incoherent, and the liability is that nobody has established otherwise.

The term is presented as motivating engineering work rather than caution: the same post lists trust engineering as one of its later subjects, proposing a three-dimensional bill of materials for the AI era as the mechanism, and frames its overall answer as delivering trustworthy software out of a mixed human-and-agent team through systematic engineering constraints.

How well established it is: this is one author's framing, stated in the opening instalment of the author's own column and offered as a diagnosis rather than a measured finding. The post gives no measurement of the debt and no method for observing it.

## Related Terms

- [[DefinedTerm/verification-debt]] — the closely neighbouring cost of unverified output
- [[DefinedTerm/comprehension-debt]] — the cost of code no one on the team has understood
- [[DefinedTerm/review-bottleneck]] — the constraint this debt is said to accumulate behind
- [[DefinedTerm/vibe-coding]] — the practice whose speed this debt is the counterpart to
