---
title: "AIに「レビューして」はもう古い？「敵対的検証」のすすめ"
type: "schema:BlogPosting"
lang: en
tags: [agentic-code-review, claude-code, sub-agents, verification]
sources:
  - type: url
    url: 'https://zenn.dev/loglass/articles/6aa18c80496ec6'
    hash: sha256:9b9653e5e191b65dccd4149229ac18d70bb58a3ca38b3b4707bddceb6d26283f
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A July 2026 Japanese-language post on the Loglass tech blog recommending that, instead of simply asking an AI to review its output, users ask for adversarial verification: a fresh-context skeptic that tries to refute the work and returns verdicts with grounds, after which a human decides which findings to accept."
  author: ["Matsuoka (little_hands)"]
  datePublished: "2026-07-17"
  publisher: "Loglass"
---

This Japanese-language post, published on the Loglass tech blog, argues for asking an AI to perform
[[DefinedTerm/adversarial-verification]] ("敵対的検証して") rather than simply to "review" its output. The author
presents it as a one-line request that gets more out of an AI reviewer: where "review this" returns a list of
points, adversarial verification assumes the work has a problem somewhere, tries to refute it, and returns a
verdict and the grounds for it. The author stresses that "review this" remains a useful prompt, and apologises
for the deliberately catchy title.

The post covers the idea's background, how the author sees it built into
[[SoftwareApplication/claude-code]], how to invoke it, how to reproduce it in other tools with a prompt
template, its limits, and a record of how the post itself was checked this way.

## Key Points

- The post defines adversarial verification as someone other than the author of a piece of work checking its
  quality by deliberately trying to refute it on the assumption that it is wrong, and traces the idea to red
  teaming, the Catholic Church's devil's advocate, and Karl Popper's falsificationism.
- It argues the approach suits AI work in particular because AI output always looks plausible — hallucinations
  and loose generalisations cannot be told apart by appearance — and the AI that produced it tends to be
  lenient with its own output, so it needs to be looked at by separate eyes cut off from the context that
  produced it.
- The author describes Claude Code's `/deep-research` as having three verification agents try to refute each
  top-ranked claim and vote, dropping claims two of three refute, and `/code-review` as having a separate agent
  re-check each finding and drop low-confidence ones; the post notes that the code-review documentation does not
  itself use the word "adversarial", that the label is the author's description of the detect, skeptically
  re-check and drop structure, and that bundled features depend on version and plan.
- According to the post, Anthropic's own published guidance for Claude Code describes adversarial verification as
  a named pattern and recommends adding an adversarial review step.
- The author attributes the effect to two things that multiply: an adversarial stance, which makes the review
  look for where the work does not hold and attach verdicts and grounds, and a fresh context, which keeps the
  reviewer from going along with the conversation that produced the work.
- In the author's own Claude Code environment, the single request started three skeptic sub-agents in parallel,
  split into reader, correctness and article-viability perspectives without being told to; the author presents
  this as an observation from one environment, which may have depended on installed skills, and suggests asking
  explicitly for sub-agents if none start.
- For tools without sub-agents, the post lists four requirements — independence, a refuting role, grounding
  factual claims in primary sources, and output a human can judge (severity and grounds for each finding) — and
  gives a prompt template to paste into a new session alongside the work alone; it states that the template's
  effect outside Claude Code has not been verified.
- It lists four limits, which it says Anthropic itself acknowledges: an adversarial reviewer reports something
  even on sound work, so chasing every finding leads to over-engineering; the opposite failure, a verifier that
  passes work without really checking it, is the one the author considers more important to guard against;
  multi-agent setups cost several times the tokens of a single agent; and a verifier using the same model shares
  its blind spots, for which the post suggests grounding in primary sources or verifying with a different model.
- Its conclusion is that AI findings are not answers: a human decides whether to accept a finding, accept a
  weakened version, or reject it, which is why verdicts and grounds matter.

## Context

The post closes with the author's own record of checking it: eight skeptics reviewed its angle, structure and
research before writing, and the author shows which findings were accepted, accepted in weakened form, or
rejected, and says seven risky statements of fact were caught in advance. The recommendations rest on the
author's experience and on vendor guidance the post cites, not on a measured comparison with plain review.
