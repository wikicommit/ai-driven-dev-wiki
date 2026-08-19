---
title: "context rot"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://www.langchain.com/blog/context-engineering-for-agents'
    hash: sha256:07e9475327ca11aeabb710cea3b419188e2ca4380d3cf4fd055291761f52fb8f
  - type: url
    url: 'https://code.claude.com/docs/en/best-practices'
    hash: sha256:92807ef3d58f63fbea435ea928df49e2f3341e118eb8c40db08800c100a4c4c5
  - type: url
    url: 'https://github.com/NeoLabHQ/context-engineering-kit'
    hash: sha256:bc2a9a7e51d46faa7b71b485a040ec8d6f6b10a78fc25f17a65dc7b9dde39b4c
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The degradation of a model's ability to accurately recall information from its context as the number of tokens in that context increases — the empirical premise behind treating context as a finite budget rather than a buffer to fill."
  termCode: ""
  inDefinedTermSet: ""
---

Context rot is the observation that as the number of tokens in a model's context window increases, its ability to accurately recall information from that context decreases. [[TechArticle/effective-context-engineering-for-ai-agents]] attributes the concept to studies on needle-in-a-haystack style benchmarking, and states that while some models degrade more gently than others, the characteristic emerges across all models. It is the empirical premise behind treating the context window as a finite resource with diminishing marginal returns rather than as a buffer to be filled up to its stated limit.

## Usage

Anthropic's stated explanation is architectural. Models are described as having an "attention budget" that every new token depletes, drawn from analogy with limited human working memory. The scarcity is traced to the transformer architecture, in which every token can attend to every other token, producing n² pairwise relationships for n tokens — so as context length grows, the model's ability to capture those relationships is stretched thin, creating a tension between context size and attention focus. A second cause given is training distribution: shorter sequences are more common than longer ones, so models have less experience with, and fewer specialised parameters for, context-wide dependencies. Techniques such as position encoding interpolation let models handle longer sequences by adapting them to the originally trained smaller context, at some cost to token position understanding. The post is careful about the shape of the effect, describing it as a performance gradient rather than a hard cliff: models remain highly capable at long contexts but show reduced precision for information retrieval and long-range reasoning.

The practical consequence is that a larger context window is not by itself a solution. Anthropic argues that for the foreseeable future context windows of all sizes will be subject to context pollution and information relevance concerns wherever the strongest agent performance is wanted.

[[BlogPosting/context-engineering]] approaches the same territory from failure modes rather than mechanism, relaying four named patterns from Drew Breunig's writing: **context poisoning**, when a hallucination makes it into the context; **context distraction**, when the context overwhelms the training; **context confusion**, when superfluous context influences the response; and **context clash**, when parts of the context disagree. It presents these alongside the more mundane costs of long context — exceeding the window, ballooning cost and latency.

Claude Code's own documentation states the practical version without the term, describing the context window as the most important resource to manage and noting that when it is getting full the model may start "forgetting" earlier instructions or making more mistakes.

## Related Terms

Context rot is the problem that [[DefinedTerm/context-engineering]] exists to manage, and the direct motivation for [[DefinedTerm/compaction]], [[DefinedTerm/agentic-memory]], and [[DefinedTerm/multi-agent-orchestration]]. [[SoftwareApplication/context-engineering-kit]] names avoiding it as the purpose of its context-isolation patterns.
