---
title: "Context rot"
type: "schema:DefinedTerm"
lang: en
tags: [agents, context-window, llm]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "The decline in a language model's ability to accurately recall information from its context as the number of tokens in the context window increases."
---

Context rot is the decline in a language model's ability to accurately recall information from
its context as the number of tokens in that context window increases. Anthropic attributes the
concept to studies on needle-in-a-haystack style benchmarking, and reports that while some models
exhibit more gentle degradation than others, the characteristic emerges across all models. Its
practical consequence is that context must be treated as a finite resource with diminishing
marginal returns rather than as a container to be filled.

## Usage
Context rot is the empirical ground Anthropic gives for [[DefinedTerm/context-engineering]]:
because recall degrades as context grows, the aim becomes finding the smallest possible set of
high-signal tokens rather than supplying everything that might conceivably be relevant. Anthropic
characterises the effect as a performance gradient rather than a hard cliff — models remain highly
capable at longer contexts but may show reduced precision for information retrieval and
long-range reasoning compared with their performance on shorter contexts.

It also shapes Anthropic's position on context-window size. Anthropic argues that waiting for
larger windows, while a tempting tactic, is unlikely to resolve the problem for the foreseeable
future, because windows of all sizes remain subject to context pollution and
information-relevance concerns wherever the strongest agent performance is wanted. The three
techniques it recommends for long-horizon work — [[DefinedTerm/compaction]],
[[DefinedTerm/structured-note-taking]] and [[DefinedTerm/sub-agent-architecture]] — are presented
as ways of addressing these constraints directly.

## Related Terms
- [[DefinedTerm/attention-budget]]
- [[DefinedTerm/context-engineering]]
