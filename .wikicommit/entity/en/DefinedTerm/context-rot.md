---
title: "Context rot"
type: "schema:DefinedTerm"
lang: en
tags: [agents, context-window, llm]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  - type: url
    url: 'https://blog.langchain.com/the-anatomy-of-an-agent-harness/'
    hash: sha256:71cffd4adc7b81b7dd5f981d26af2bebcee592b2751a882ea95bb833fa2d022e
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

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

A later post on long-running agents names context rot, alongside a context window's hard token limit, as one of the reasons a multi-hour or multi-day agent run cannot simply rely on an ever-larger context window: the degradation is said to kick in well before that hard limit is reached.

LangChain's [[BlogPosting/the-anatomy-of-an-agent-harness]] uses the term, linking to research by Chroma,
for models becoming worse at reasoning and completing tasks as their context window fills up, and treats it
as a problem the agent harness has to manage — describing harnesses today as largely delivery mechanisms for
good context engineering. It names three harness strategies: [[DefinedTerm/compaction]], which summarizes
and offloads the context when the window is nearly full; [[DefinedTerm/tool-call-offloading]], which keeps
only the head and tail of large tool outputs in context and writes the rest to the filesystem; and Skills,
which use [[DefinedTerm/progressive-disclosure]] so that too many tools or MCP servers are not loaded into
context at the start, where they would degrade performance before the agent begins work.

## Related Terms

- [[DefinedTerm/attention-budget]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/long-running-agent]]
- [[DefinedTerm/tool-call-offloading]]
- [[DefinedTerm/agent-harness]]
