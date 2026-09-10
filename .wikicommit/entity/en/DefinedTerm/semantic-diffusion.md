---
title: "Semantic Diffusion"
type: "schema:DefinedTerm"
lang: en
tags: [terminology, software-engineering]
sources:
  - type: url
    url: https://simonwillison.net/2025/Mar/23/semantic-diffusion/
    hash: sha256:472ba908e669a42742696d92e042aca8106e1995d7e09841e4452b160c3bb490
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "The weakening of a term's definition as it spreads beyond the people who coined it. Coined by Martin Fowler in 2006 and applied here to the reception of vibe coding, whose narrow original meaning was reported as already being displaced by a looser one."
---

Semantic diffusion is what happens to a word that was coined by a person or group with a reasonably
good definition and then spreads through the wider community in a way that weakens that definition —
a weakening that risks losing the definition entirely, and with it any usefulness the term had. The
term was coined by Martin Fowler in 2006, who described the mechanism as essentially a succession of
the telephone game, in which people other than a term's originators start talking about it without
being careful to follow the original definition. It names a failure mode in technical vocabulary
rather than a practice anyone carries out deliberately.

## Usage
The term is used to diagnose why a piece of jargon has stopped being useful: not that it was badly
defined at the outset, but that the definition did not survive the journey to its wider audience.
Simon Willison, writing in March 2025, presents the reception of [[DefinedTerm/vibe-coding]] as an
instance of the effect — he had been complaining that the term was already being distorted to mean
any time an LLM writes code, as against its intended meaning of code written with an LLM without the
person reviewing what was written, and encountered Fowler's term in the course of that complaint.
His own account of the frustration is that "for a few glorious moments we had the chance at having
ONE piece of AI-related terminology with a clear, widely accepted definition", and that people could
not be trusted to read Andrej Karpathy's original post all the way to the end. He reports the same
thing having happened to his own coinage, [[DefinedTerm/prompt-injection]], over the preceding couple
of years.

Willison regards this dilution of meaning as frustrating but apparently inevitable, and — attributing
the point to Fowler — notes that it is most likely to happen to popular terms, on the reasoning that
the more popular a term is, the higher the chance of a game of telephone in which misunderstandings
multiply as the chain grows. What the effect does not appear to be is something a term's originator
can simply overrule: Karpathy, who coined vibe coding, replied to Willison's article that it will
take time to settle on definitions, and described his own practice as rarely going full out vibe
coding — more often still looking at the code, adding complexity slowly, and trying to learn how the
pieces work.

## Related Terms
- [[DefinedTerm/vibe-coding]] — the term whose dilution is presented here as a current example
- [[DefinedTerm/prompt-injection]] — an earlier coinage the same source reports as having undergone
  the same effect
