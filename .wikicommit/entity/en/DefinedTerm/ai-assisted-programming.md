---
title: "AI-Assisted Programming"
type: "schema:DefinedTerm"
lang: en
tags: [llm, software-engineering]
sources:
  - type: url
    url: https://simonwillison.net/2025/Mar/19/vibe-coding/
    hash: sha256:653ba52b66ad62da601ae6fd257897841726d7ac6a07029edc6d0e1c5b12188f
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "The general practice of writing software with the help of large language models, of which vibe coding is one narrow subset. Distinguished from vibe coding by whether the developer reads, tests, and can explain the code before relying on it."
---

AI-assisted programming is the general practice of writing software with the help of large language
models. It is used here as the umbrella category that
[[DefinedTerm/vibe-coding]] falls under rather than as a synonym for it: in
[[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]], Simon Willison argues that
collapsing the two dilutes the narrower term and gives a false impression of what is possible when
LLMs are used responsibly. The distinguishing question is not which model or editor was used but
whether the code is reviewed — an LLM's involvement in producing code that was then read, tested,
and understood is, on this account, immaterial to what the activity is.

## Usage
The term is invoked in this source mainly to mark out what professional practice requires that
unreviewed generation does not. Willison frames a developer's job as more than producing code and
features: the code has to demonstrably work, be understandable to other humans and machines, and
support continued development afterwards. That brings in performance, accessibility, security,
maintainability, and cost efficiency, and he characterises software engineering as the business of
picking among many possible solutions by balancing explicit and implied requirements against each
other.

His stated personal rule for production-quality work of this kind is that he will not commit code
to his repository if he could not explain exactly what it does to somebody else. He describes this
as his own golden rule rather than as an industry convention, and notes that he has written
separately about his own process at greater length.

## When It Applies
The framing is aimed at code intended to be relied on and maintained — anything where the criteria
above apply — as opposed to the low-stakes prototypes and throwaway projects that
[[DefinedTerm/vibe-coding]] is defended for. It assumes the developer is able to read and evaluate
what the model produced; where that ability or that intent is absent, the activity is the narrower
one under a broader name, which is the confusion the source is written to correct.

Willison also observes that working effectively this way is genuinely difficult: knowing what does
and does not work is a matter of building intuition over time, with hidden sharp edges along the
way. That claim, and the golden rule above, are one practitioner's account of his own practice
rather than a measured or widely-agreed standard.

## Related Terms
- [[DefinedTerm/vibe-coding]] — the subset of this practice in which the code is not reviewed
