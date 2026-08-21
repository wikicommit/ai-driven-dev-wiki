---
title: "context engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05344'
    hash: sha256:29a5dfd46c7505affc599f6922ebba2f67d01e7f3a343df5347a42f435a08edc
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://www.langchain.com/blog/context-engineering-for-agents'
    hash: sha256:07e9475327ca11aeabb710cea3b419188e2ca4380d3cf4fd055291761f52fb8f
  - type: url
    url: 'https://github.com/NeoLabHQ/context-engineering-kit'
    hash: sha256:bc2a9a7e51d46faa7b71b485a040ec8d6f6b10a78fc25f17a65dc7b9dde39b4c
  - type: url
    url: 'https://code.claude.com/docs/en/best-practices'
    hash: sha256:92807ef3d58f63fbea435ea928df49e2f3341e118eb8c40db08800c100a4c4c5
  - type: url
    url: 'https://www.anthropic.com/engineering/writing-tools-for-agents'
    hash: sha256:effc06d088266ee895582c23541e543435288246b1dc4d89d3a2f4b8a1993b54
  - type: url
    url: 'https://sourcegraph.com/blog/context-engineering'
    hash: sha256:004e8195be79c691c84abc9a3ab6d698b8815f7ee396e367c8aca94f56715dc3
  - type: url
    url: 'https://arxiv.org/pdf/2601.21557'
    hash: sha256:dbbe563536036bbc57c25fc8000ec69a87e78fc39649b404f944758b9d48e086
  - type: url
    url: 'https://simonwillison.net/2026/Feb/9/structured-context-engineering-for-file-native-agentic-systems/'
    hash: sha256:3f82de188c24399ccbce66e5e53af94f0076aa296322a4b9d6a662e0554d1406
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The engineering discipline concerned with what an LLM-based agent is allowed to see in its context window — which instructions it receives, how much history is retained, what it has learned from prior interactions, and how external information is assembled before each model call."
---

Context engineering is the set of mechanisms that manage what an LLM-based agent sees in its context window. [[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] states the premise directly: agents do not simply send user messages to a model and receive responses, and the quality of every response is determined primarily by which instructions the model receives, how much conversation history is retained, what it has learned from prior interactions, and how relevant external information is assembled before each call.

## Practitioner definitions

Two widely circulated 2025 posts define the term from the vendor side, arriving at compatible accounts organised differently.

[[TechArticle/effective-context-engineering-for-ai-agents]] presents context engineering as the natural progression of prompt engineering: where prompt engineering concerns writing and organising instructions — mostly system prompts — context engineering is the set of strategies for curating and maintaining the optimal set of tokens during inference, including everything that lands in the window outside the prompts. Its stated shift is from asking which words to write to asking "what configuration of context is most likely to generate our model's desired behavior?" It grounds this in an argument about attention rather than about token limits, treating context as a finite resource with diminishing marginal returns because every token depletes an "attention budget" (see [[DefinedTerm/context-rot]]), and distills its guidance to a single principle: find the smallest possible set of high-signal tokens that maximise the likelihood of the desired outcome. Its practical prescriptions cover system prompts at the "right altitude" — between brittle hardcoded if-else logic and vague guidance that falsely assumes shared context — tool sets small enough that a human could say which tool applies in a given situation, curated canonical examples rather than exhaustive edge-case lists, and just-in-time retrieval in which the agent holds lightweight identifiers such as file paths and loads data at runtime rather than pre-processing everything up front.

[[BlogPosting/context-engineering]] organises the same territory as four things you can do with context — **write** it outside the window, **select** it back in, **compress** it to only what a task needs, and **isolate** it across agents, sandboxes, or state fields — and populates each bucket with examples from shipped agents and papers. It divides the context to be managed into instructions, knowledge, and tools, and takes its framing from Andrej Karpathy's analogy of the model as a CPU and the context window as RAM.

Where the two differ is in emphasis rather than substance: Anthropic argues from model behaviour toward a minimality principle, while LangChain surveys practice toward a set of categories. Both name the same three techniques for work that outlasts a context window — [[DefinedTerm/compaction]], [[DefinedTerm/agentic-memory]], and [[DefinedTerm/multi-agent-orchestration]]; LangChain additionally frames tracing and token-usage tracking as prerequisites, so that the effect of any context-engineering change can be tested.

The term has also become a product category. [[SoftwareApplication/context-engineering-kit]] packages context engineering techniques as installable plugins, and its stated design criteria — a minimal token footprint, granular installation so unused plugins load nothing, and preferring command-oriented skills with subagents over general information skills — are themselves applications of the minimality principle to the agent's own configuration.

## Usage

The report summarizes a formal taxonomy from the context engineering survey literature that treats the context supplied to a model as a structured tuple assembled from instructional context, external knowledge, tool schemas, memory, execution state, and the user query, organized around three pillars: *context retrieval* (selecting relevant information from external sources), *context processing* (transforming, compressing, or restructuring retrieved content), and *context management* (maintaining coherence and relevance across turns).

It also summarizes a historical framing from work on "context engineering 2.0", which traces four eras — early prompt engineering focused on single-turn instruction, retrieval-augmented generation that introduced external knowledge, tool-augmented agents that expanded the action space, and a current era that treats context as a first-class engineering concern — and articulates three guiding principles: *entropy reduction*, that each context element should reduce uncertainty about the desired output; *minimal sufficiency*, that only what is necessary should be included to avoid attention dilution; and *semantic continuity*, that context should evolve coherently across turns rather than being reconstructed from scratch. That work also identifies a narrowness gap in current systems, which the report describes as an overwhelming focus on chat history management while neglecting holistic dimensions such as tool state, environmental signals, and cross-session knowledge.

In practice the report treats context as the central design constraint of a long-running agent. Its stated experience is that tool outputs — file contents, command results, search hits — consume 70–80% of the context in a typical session, dwarfing the system prompt and the agent's own reasoning, which makes context utilization the single most important metric for agent longevity and imposes a pervasive tension: richer tool outputs improve per-turn accuracy but shorten the session's useful life.

Concrete techniques the report groups under the discipline include:

- **Conditional prompt composition** — factoring behavioral instructions into independent sections with a condition predicate and a priority, so that irrelevant sections are excluded before any file is read
- **Prompt structure for caching** — splitting the system prompt into a stable prefix and a dynamic suffix so the prefix can be cached across a multi-turn session
- **Tool result optimization** — replacing raw outputs with compact summaries, and offloading outputs above a size threshold to scratch files with a preview and a reference path
- **Dual-memory architecture** — supplying a thinking model with a compressed episodic summary of the full history alongside verbatim recent messages
- [[DefinedTerm/adaptive-context-compaction]] — graduated reduction stages applied as context pressure rises
- [[DefinedTerm/system-reminders]] — short, targeted messages injected at the point of decision to counteract attention decay
- **An experience-driven memory pipeline** — accumulating project-specific knowledge as a playbook of natural-language bullets scored by effectiveness, recency, and semantic similarity

Two lessons the report draws are framed as broadly applicable. The first is to treat context as a budget rather than a buffer, designing graduated reduction stages instead of a single emergency compaction at a hard limit. The second is to calibrate from API-reported token counts rather than local estimates, because providers inject invisible content — safety preambles, tool schema serializations, internal formatting — that makes local counting systematically underestimate actual usage; in the author's system that discrepancy was large enough to cause compaction to trigger too late and produce context overflow errors.

The report also notes a finding from the survey literature it treats as a design lever: LLMs are more robust to compressed context during understanding tasks than during generation tasks, which suggests aggressive compression is most viable for context that informs reasoning rather than context that directly shapes output text.

The tool layer is a context-engineering surface in its own right, not only a capability layer. [[TechArticle/writing-effective-tools-for-agents]] applies the same minimality reasoning to what tools return: because an agent's context is limited where computer memory is cheap and abundant, a tool that returns everything forces the agent to spend context reading through irrelevant material, so tools should be chosen and shaped to return only high-signal information. Its concrete prescriptions are of a piece with the definitions above — prefer a `search_contacts` tool over a `list_contacts` tool, consolidate frequently chained operations into a single call so intermediate outputs never enter the context, drop low-level identifiers such as `uuid` and `mime_type` in favour of fields an agent will actually act on, and apply pagination, filtering and truncation with sensible defaults, with Claude Code restricting tool responses to 25,000 tokens by default. It also treats the tool's own text as context to be engineered: descriptions, specs and even error messages are loaded into the agent's window and therefore steer behaviour, which puts them under the same budget as everything else.

### Four pillars, and the line against prompt engineering

[[BlogPosting/context-engineering-a-practical-guide-for-ai-agents]] offers an organisation of the discipline rather than a new definition, and is candid that the carving is a choice: it notes that other authors list hierarchical layers, or seven components, or walk through the parts without enumerating them, and proposes four pillars as a practical alternative. **Instructions** — role, constraints, and output format before the first user message, where its stated failure mode is not length but a mismatch with the model's training, since instructions contradicting the model's default tool-use heuristics confuse it every turn. **Retrieval** — how external data enters the window, whether through RAG, structured queries, file reads, or just-in-time loading. **Memory** — short-term conversation history and long-term cross-session state, usually with a compaction step. **Tools** — the executable surface, described as where the discipline "gets the most ruthless," since every definition and every result costs tokens and near-duplicate tools force the model to burn turns choosing.

Its contribution to the prompt-engineering comparison above is a usable test rather than a taxonomy: "If you're swapping nouns and adjectives, you're still doing prompt engineering. If you're changing what data the agent retrieves, in what order, with what re-ranking, and what gets evicted when the context window fills, you're doing context engineering." The four questions it reduces the discipline to are what to fetch, when to fetch it, how to compress it, and when to throw it away.

Two mechanisms it emphasises are absent from the vendor accounts above. **Token budget management** is defined there as cutting low-signal content *before* it enters the window rather than after — truncating tool outputs, compacting old turns, dropping retrieved chunks below a relevance threshold, and capping how many candidates each retrieval call contributes. **Re-ranking** is presented as the step where naive RAG pipelines either start or stop working, with a smaller cross-encoder or cheap model scoring candidates and keeping a precise top-k; its illustration is retrieving 50 candidates at high recall and re-ranking to five rather than dumping all 50 into the prompt.

The post also brings ordering into the discipline, quoting the Liu et al. "lost in the middle" finding that performance "is often highest when relevant information occurs at the beginning or end of the input context, and significantly degrades when models must access relevant information in the middle of long contexts, even for explicitly long-context models" — with the practical consequence that assembly order matters, and the highest-signal material belongs at the top or bottom rather than buried. That paper is not itself among this page's sources; the finding is recorded as the guide's citation of it.

On attribution of the term itself, this guide credits Phil Schmid with helping popularize it in mid-2025 — which sits alongside, rather than against, [[BlogPosting/skill-issue-harness-engineering-for-coding-agents]] crediting the coinage to its author's cofounder Dex Horthy in the 12-factor agents work. That post also proposes [[DefinedTerm/harness-engineering]] as a named subset of this discipline: the part that works specifically through the agent's configuration points.

### Optimising the procedure, not just the content

Every account above fixes a procedure and then reasons about what should flow through it. [[ScholarlyArticle/meta-context-engineering]] argues that fixing the procedure is itself the limiting choice: current methods "rely on manually crafted harnesses, such as rigid generation-reflection workflows and predefined context schemas," which "impose structural biases and restrict context optimization to a narrow, intuition-bound design space." Its named example of what it supersedes is the generation–reflection–curation workflow of [[ScholarlyArticle/agentic-context-engineering]].

Its proposal splits the work across two levels. A meta-level agent evolves the context-engineering *skills* through what it calls agentic crossover — a deliberative search over the history of skills, their executions, and their evaluations — using [[DefinedTerm/agent-skills]] as the unit being evolved. A base-level agent then applies those skills, and rather than filling a predefined schema it "leverages coding toolkits and filesystem access to instantiate and optimize context as flexible, programmatic artifacts." The reported gains over prior agentic context-engineering methods are 5.6–53.8% relative, with a mean of 16.9%, across five domains and four models; that spread suggests how much the payoff depends on the domain, and the figures are the authors' own against their own baselines.

### Encoding, not just selection

Most accounts of context engineering concern *what* reaches the model. A link post by [[Person/simon-willison]] surfaces a study concerned with *how it is written down*, using SQL generation as a proxy for programmatic agent operations across 9,649 experiments, 11 models, four formats (YAML, Markdown, JSON and Token-Oriented Object Notation) and schemas ranging from 10 to 10,000 tables.

Two of its results are relayed there. First, the largest effect was the model itself: frontier models outperformed the leading open-source models, and only the frontier models benefited convincingly from filesystem-based context retrieval — which Willison reads as reinforcing his sense that filesystem coding-agent loops are not yet handled as well by open-weight models. Second, the [[DefinedTerm/grep-tax]] result, in which a format roughly 25% smaller on disk consumed 138% more tokens than YAML at 500 tables and 740% more at 10,000, because the models could not construct effective refinement patterns in a syntax they were unfamiliar with.

The practical lesson that follows is that a format's token count in isolation is the wrong measure: what matters is how cheaply a model can iterate against it.

### As a role, not only a practice

[[BlogPosting/context-engineering-a-practical-guide-for-ai-agents]] also names an owner. A *context engineer*, in its definition, is "the person (or role on a platform team) responsible for the architecture that feeds AI systems the right context at the right time," with work spanning retrieval pipelines, memory systems including long-term memory, tool design, and evaluation — sitting "closer to systems engineering than to prompt writing."

Its comparison table assigns ownership on the same axis it uses to separate the two disciplines: prompt engineering belongs to "anyone writing prompts," while context engineering belongs to the "platform team building the agent pipeline." That is a claim about where the work sits in an organisation rather than only about what the work is, and it is this vendor's framing rather than an established job definition.

## Related Terms

Context engineering is one of the concerns coordinated by the [[DefinedTerm/agent-harness]] at runtime, while the modular system prompt it manages is assembled during [[DefinedTerm/agent-scaffolding]]. The problem it exists to manage is [[DefinedTerm/context-rot]]; its principal techniques are [[DefinedTerm/compaction]], [[DefinedTerm/agentic-memory]], and [[DefinedTerm/multi-agent-orchestration]]; and the simplest always-loaded form of it is covered under [[DefinedTerm/context-files]]. End users of a [[DefinedTerm/coding-agent]] meet the same discipline as session hygiene: Claude Code's documentation frames its recommendations around the context window as the fundamental constraint, prescribing `/clear` between unrelated tasks, `/compact` with instructions, and delegation to [[DefinedTerm/subagents]] so that exploration does not consume the main conversation. The report also surveys meta-level work that treats context engineering itself as an optimization problem rather than a manual design task, searching over context configurations such as system prompts, tool schemas, and memory strategies.
