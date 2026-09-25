---
title: "Verification Ladder"
type: "schema:DefinedTerm"
lang: en
tags: [loop-engineering, verification]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.00038'
    hash: sha256:2f17c51102988847128a0fb57824555d6ac3a32183f9ed61e269f1a63d48d4c0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A five-level scale of how rigorously an agent loop verifies its result, from deterministic checks (level 1) through rules, delayed field truth and a model as judge, to a human checkpoint (level 5)."
---

The verification ladder is a five-level scale for classifying how rigorously a
[[DefinedTerm/loop-specification]] checks whether its work is done, proposed in
[[ScholarlyArticle/stop-hand-holding-your-coding-agent]] as a refinement of the simpler split
between verifiable and judged goals. Level 1 is **deterministic**: an assertion, an exit code, a
golden output. Level 2 is a **rule or constraint** over the text: a linter, a schema, a policy.
Level 3 is **delayed field truth**: tests, a deploy, a real customer response — true but slow.
Level 4 is a **model as judge**, scoring by rubric, which is the model's opinion rather than field
truth. Level 5 is a **human checkpoint**, which the paper calls supervision rather than automated
verification. Levels 1 and 2 form the autonomous zone of checks that run immediately on their own,
levels 1 through 3 the objective zone, and levels 4 and 5 assisted flow, in which a model or a human
stands in for a check.

## Usage

The paper states the message organizing the ladder as a discipline of honesty: do not pretend that
level 4 is level 1. A loop is only as autonomous as the level its verifier truly sits at, and when a
level-4 judge is unavoidable, a different model should judge rather than the same agent approving
itself — the maker–checker split. It lists "pretending level 4 is level 1" among its anti-patterns,
citing surveys of [[DefinedTerm/llm-as-a-judge]] on the biases and prompt sensitivity of model
judges.

The paper also uses the ladder descriptively. Coding the dominant verification level of each of the
fifty loops in the public Loop Library catalogue, it reports that half verify at level 1 and a fifth
at level 2, so that seventy percent sit in the autonomous zone and seventy-six percent within the
objective zone; twenty-two percent rely on a level-4 judge, and a single loop uses a human checkpoint
as its dominant verification. It reads this as descriptive support for practitioners preferring
objective checks and treating the model judge as a hardened exception.

## Related Terms

[[DefinedTerm/loop-specification]], [[DefinedTerm/loop-engineering]],
[[DefinedTerm/llm-as-a-judge]], [[DefinedTerm/verification-loop]]
