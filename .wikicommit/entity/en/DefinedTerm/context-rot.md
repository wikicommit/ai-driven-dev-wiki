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
  - type: url
    url: 'https://arxiv.org/pdf/2510.04618'
    hash: sha256:6b917acfae2be76706c1360bd37b74776f6c979139cfb5a5604b5f0ed5f78951
  - type: url
    url: 'https://arxiv.org/pdf/2602.07962'
    hash: sha256:795a9ba68ee512a5cd028441b92ad7ecf110f3ae5db70692b69b065e92a2a77a
  - type: url
    url: 'https://arxiv.org/pdf/2606.27045'
    hash: sha256:9004fd8330acfa64f27d8cc588f1234dd91b29303e4ee479b537bbdebca481f6
  - type: url
    url: 'https://nyosegawa.com/en/posts/coding-agent-workflow-2026/'
    hash: sha256:bb7d36388cc5d0dc91fc90185585f6fff68833b1b198e732c6e2d6d41a285f45
review_status: pending
generated_at: "2026-08-21"
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

A distinction worth preserving as this vocabulary grows: context rot is degradation of *recall over material that is still present*. [[ScholarlyArticle/agentic-context-engineering]] names two failures with the opposite shape, where the material itself stops being there — [[DefinedTerm/context-collapse]], the abrupt compression of an accumulated context when a model rewrites it wholesale, and **brevity bias**, the slower drift of iterative optimization "toward short, generic prompts" that omit domain-specific detail and propagate their seeds' faults across iterations. Remedies aimed at one do not address the other: a larger window or better attention does nothing about a summary that deleted the content, and an append-only update discipline does nothing about attention thinning over a window that is genuinely full.

### Measuring it in an agentic setting

The needle-in-a-haystack studies the accounts above rest on measure recall from a long passage handed to the model. [[ScholarlyArticle/loca-bench]] argues that this understates the problem for agents, because an agent's context is not given to it — the agent builds it, by exploring an environment it starts out knowing little about. Its reframing is that "the core difficulty is not just finding the right evidence once, but remaining organized and reliable at every action as the context grows over time."

Its benchmark, [[Dataset/loca-bench]], turns that into a controlled measurement by scaling the *environment* — the size of a spreadsheet, a PDF, a database — while holding the task prompt and semantics fixed, so context length can be extended arbitrarily without making the task harder. The reported curve is steep: most models score above 70% at short context, then "performance drops sharply even though the underlying task does not change," with the gap between frontier and open-source models widening as it does.

That work also separates four failure dimensions that the recall framing collapses into one: multi-piece retrieval and joint reasoning; instruction following, where agents "frequently forget earlier instructions" among multi-constraint tasks; exploration, where agents are reported to explore less and behave more conservatively as context lengthens; and hallucination, where longer contexts are reported to produce subtle alterations of factual detail. And it reports that context engineering strategies recover a substantial part of the loss but unevenly — frontier models generally benefiting more from them than open-source ones — which makes the scaffold part of what any such measurement is actually measuring.

### Heuristic and evidence, kept apart

[[ScholarlyArticle/the-spec-growth-engine]] is unusually careful about which parts of the practitioner picture are supported. It records that practitioners shorthand the high-fill regime as the **Dumb Zone**, with an often-quoted rule of thumb to become cautious past roughly 40% context fill and not to treat the last ~60% as a working zone — and then states plainly that this is a rule of thumb from coding-agent practice rather than a proven threshold, with the exact point depending on model and task.

The underlying effect it treats as well supported by research, citing findings that models use long contexts unevenly and retrieve worst from the middle, that quality falls consistently as input grows, and that on long-context coding specifically a strong model dropped from 29% to 3% on a software-engineering benchmark as the window grew from 32K to 256K tokens. Its stated takeaway is directional rather than numerical: less, well-chosen context beats more.

That paper's practical consequences of an unscoped context are architectural rather than statistical. An agent given the whole repository conflates concerns from unrelated modules and produces "global fixes" that touch boundaries it was not asked to change; and the root cause it names is that there is no principled way to tell an agent it may know exactly one thing and nothing more, leaving a developer to either give everything or guess. Its answer is the [[DefinedTerm/spine]], which derives the scope from the architecture instead.

### How much headroom the 1M-token generation bought

[[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] gives a practitioner's reading of where the problem stands as of March 2026. It restates the core finding — that output quality degrades measurably as input context length grows, with performance dropping continuously long before the token limit is reached — citing Chroma Research and Morph. It then records what changed: Claude (Opus 4.6 and Sonnet 4.6) and Codex support a 1M-token context window, and Opus 4.6 scored 78.3% on MRCR v2, which that post describes as the top score among frontier models for long-context retrieval. Its stated conclusion is careful: context rot has not disappeared, but the practical headroom has expanded significantly.

Its practical advice is unchanged by that expansion. Keep sessions short, treating one session per task as the rule and starting fresh at each phase boundary. Delegate research and exploration to [[DefinedTerm/subagents]] so the main context is not polluted. Do not fear [[DefinedTerm/compaction]]. And do not load files "just in case," since bulk loading backfires. The post's own framing of the choice is that whether to keep sessions short or deliberately exploit a long window depends on the task — it notes that a 1M context can be enabled explicitly in Codex and runs by default for Opus 4.6 on one Claude Code plan, with an environment variable to turn it off.

## Related Terms

Context rot is the problem that [[DefinedTerm/context-engineering]] exists to manage, and the direct motivation for [[DefinedTerm/compaction]], [[DefinedTerm/agentic-memory]], and [[DefinedTerm/multi-agent-orchestration]]. [[SoftwareApplication/context-engineering-kit]] names avoiding it as the purpose of its context-isolation patterns.
