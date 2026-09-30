---
title: "Adversarial verification"
type: "schema:DefinedTerm"
lang: en
aliases: ["敵対的検証"]
tags: [agentic-code-review, verification, sub-agents]
sources:
  - type: url
    url: 'https://zenn.dev/loglass/articles/6aa18c80496ec6'
    hash: sha256:9b9653e5e191b65dccd4149229ac18d70bb58a3ca38b3b4707bddceb6d26283f
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "Checking the quality of a piece of work by having someone other than its author deliberately try to refute it on the assumption that it is wrong, applied to AI output by giving a fresh-context reviewer a skeptic's role and asking for verdicts and grounds rather than a list of suggestions."
---

Adversarial verification is, as defined in [[BlogPosting/adversarial-verification-instead-of-asking-ai-to-review]],
checking the quality of a piece of work by having someone other than the one who produced it deliberately try to
refute it, on the assumption that it is wrong somewhere. Applied to AI output, it means handing the work to a
reviewer — typically a sub-agent with a fresh context — whose role is to break the work's claims, premises and
conclusions rather than to suggest improvements, and which returns a verdict and its grounds for each finding.
That post contrasts it with simply asking an AI to "review" something, which it says also returns useful points
but does not start from the assumption that something is wrong.

## Usage

The post traces the underlying idea to older practices — red teaming, the devil's advocate in the Catholic
Church's canonization process, and Popper's falsificationism — whose shared structure it describes as attacking
a conclusion from the opposite side on purpose in order to make it stronger. It argues that AI work needs this
because AI output always looks plausible and the model that produced it tends to be lenient with it.

In [[SoftwareApplication/claude-code]], the post's author describes the pattern as already present in built-in
features: `/deep-research`, in which several agents try to refute each important claim and vote, and
`/code-review`, in which a separate agent re-checks each finding and low-confidence findings are dropped. The
author notes that the code-review documentation does not itself use the word "adversarial" and that the label is
a description of that structure. According to the post, Anthropic's own guidance for Claude Code also describes
adversarial verification as a named pattern and recommends adding an adversarial review step. In the author's
environment, a one-line request to "adversarially verify" a draft started several skeptic sub-agents on its own;
the author reports this as one environment's behaviour.

## When It Applies

The post names four requirements for the approach to work: independence (a reviewer cut off from the context
that produced the work), a refuting role rather than a reviewing one, grounding factual claims in primary sources
rather than the model's memory, and output a human can judge, with a severity and grounds for each finding. Where
a tool has no sub-agents, it suggests meeting the first requirement by opening a new session and pasting in only
the work, not its history. It recommends the approach for work that is expensive to redo — articles before
publication, decision documents, code before release — and for checking research, design notes, proposals and
ADRs.

It also sets out how it fails. An adversarial reviewer will report findings even on sound work, and chasing all of
them leads to over-engineering; a verifier may instead pass work without really checking it, which the author
considers the more dangerous failure because adversarial output looks convincing; multi-agent verification costs
several times the tokens of a single agent; and a verifier using the same model as the author shares its blind
spots, which the post suggests countering with grounding in primary sources or a different model (see
[[DefinedTerm/cross-model-review]]). The post's conclusion is that a human still decides whether to accept,
weaken or reject each finding. Its recommendations rest on one practitioner's experience and on vendor guidance it
cites, not on a measured comparison.

## Related Terms

- [[DefinedTerm/cross-model-review]] — having a different model review the work, one of the post's remedies for shared blind spots
- [[DefinedTerm/review-finding-triage]] — judging each review finding before acting on it
- [[DefinedTerm/sub-agent-architecture]] — the fresh-context sub-agents the pattern relies on in Claude Code
- [[DefinedTerm/review-loop-non-convergence]] — what can follow when every finding from a gap-seeking reviewer is acted on
