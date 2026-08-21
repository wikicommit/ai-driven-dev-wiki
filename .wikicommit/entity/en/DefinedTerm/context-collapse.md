---
title: "context collapse"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2510.04618'
    hash: sha256:6b917acfae2be76706c1360bd37b74776f6c979139cfb5a5604b5f0ed5f78951
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The abrupt compression of an accumulated context into a much shorter, less informative summary when a model is asked to rewrite it wholesale — named in an ICLR 2026 paper, which reports a case where a context fell from 18,282 tokens to 122 in a single step and accuracy dropped below the no-adaptation baseline."
  termCode: ""
  inDefinedTermSet: ""
---

Context collapse is the term [[ScholarlyArticle/agentic-context-engineering]] gives to what happens when a large accumulated context is regenerated in full by a model: rather than reproducing what it was given, the model compresses it into a much shorter, less informative summary, "causing a dramatic loss of information." The paper's framing is that this is not a bug in any one method but "a fundamental risk of end-to-end context rewriting with LLMs, where accumulated knowledge can be abruptly erased instead of preserved."

## Usage

The case that names the phenomenon is a single-step cliff rather than a gradual decline. In the paper's AppWorld case study, at adaptation step 60 the context held 18,282 tokens and reached 66.7 accuracy; at the next step it collapsed to 122 tokens and 57.1 accuracy — worse than the 63.7 the same setup achieved with no accumulated context at all. That last comparison is the important one: the collapse did not merely undo the adaptation, it left the system worse off than never having adapted.

The paper pairs collapse with a slower-acting sibling it calls **brevity bias**: "the tendency of optimization to collapse toward short, generic prompts." Where collapse is one catastrophic rewrite, brevity bias is iterative erosion toward generic instructions that omit domain-specific detail — and, because each optimized prompt inherits its seed's faults, propagates recurring errors across iterations rather than correcting them. Both undermine domains where success depends on accumulating rather than compressing task-specific insight.

The structural remedy the paper proposes follows from the diagnosis: stop rewriting. Its ACE framework has a Curator emit compact **delta entries** that are merged deterministically into the existing context, so no step ever regenerates the whole — nothing can be dropped because nothing is rewritten.

## Related Terms

Context collapse sits in a family of lossy-context failures that are worth keeping distinct. [[DefinedTerm/context-rot]] concerns degraded recall of material that is still present in the window; collapse concerns material that has been removed by a rewrite. [[DefinedTerm/governance-decay]] is a targeted instance of removal — a summarization step dropping standing policies specifically — while collapse is indiscriminate. The operation in which collapse occurs is [[DefinedTerm/compaction]], and the append-only-delta answer to it stands against the summarize-and-continue approach that vendor implementations of compaction take. Where the accumulated context is being maintained deliberately as a durable artifact, see [[DefinedTerm/agentic-memory]].
