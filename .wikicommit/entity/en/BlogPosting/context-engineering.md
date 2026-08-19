---
title: "Context Engineering"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, agent-architecture, agentic-coding]
sources:
  - type: url
    url: 'https://www.langchain.com/blog/context-engineering-for-agents'
    hash: sha256:07e9475327ca11aeabb710cea3b419188e2ca4380d3cf4fd055291761f52fb8f
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A 2 July 2025 LangChain post that groups [[DefinedTerm/context-engineering]] strategies into four buckets — write, select, compress, and isolate — with examples drawn from popular agents and papers, then maps each onto LangGraph."
  author:
    - "The LangChain Team"
  datePublished: "2025-07-02"
  publisher: "LangChain"
---

"Context Engineering" is a post published by the LangChain team on 2 July 2025. Its organising contribution is a four-bucket taxonomy of [[DefinedTerm/context-engineering]] strategies — **write, select, compress, and isolate** — assembled from a review of popular agent products and papers, with the second half of the post mapping each bucket onto features of [[SoftwareApplication/langgraph]].

The post opens with an analogy it attributes to Andrej Karpathy, that LLMs are like a new kind of operating system in which the model is the CPU and the context window is the RAM, and quotes his description of context engineering as the "delicate art and science of filling the context window with just the right information for the next step." It divides the context that must be managed into instructions (prompts, memories, few-shot examples, tool descriptions), knowledge (facts and memories), and tools (feedback from tool calls).

It is a vendor post: the taxonomy is presented as a survey of what practitioners are doing, but the second half is an argument that LangGraph's design supports each bucket.

## Key Points

- **Why it matters.** Long-running tasks and accumulating tool feedback mean agents use large numbers of tokens, which can exceed the context window, balloon cost and latency, or degrade performance. The post relays four named failure modes from Drew Breunig's writing — context poisoning (a hallucination entering the context), context distraction (context overwhelming training), context confusion (superfluous context influencing the response), and context clash (parts of the context disagreeing). See [[DefinedTerm/context-rot]].
- **Write:** saving context outside the context window. Scratchpads persist information during a task, implemented either as a tool that writes to a file or as a field in a runtime state object; memories persist across sessions. The post cites Reflexion's idea of reflecting after each agent turn and reusing the self-generated memories, and Generative Agents' periodic synthesis of memories from past feedback, and notes that ChatGPT, Cursor, and Windsurf all auto-generate long-term memories. See [[DefinedTerm/agentic-memory]].
- **Select:** pulling context into the window. It distinguishes episodic (few-shot examples), procedural (instructions), and semantic (facts) memory types, and observes that many code agents sidestep the selection problem by always pulling in a narrow set of files — naming `CLAUDE.md` for Claude Code and rules files for Cursor and Windsurf. It also covers RAG over tool descriptions to avoid overloading an agent with too many tools, and relays a quote from Varun at Windsurf that indexing code is not the same as context retrieval, with embedding search becoming unreliable as a codebase grows.
- **Compress:** retaining only the tokens required. Summarization across an agent trajectory — the post points to Claude Code's auto-compact behaviour as a familiar example — plus summarization applied at specific points such as after token-heavy tool calls or at agent-to-agent boundaries. Trimming is distinguished from summarization as filtering or pruning by heuristic rather than by model. See [[DefinedTerm/compaction]].
- **Isolate:** splitting context up. Splitting across sub-agents, each with its own tools, instructions, and context window, is described as the most popular approach; the post relays Anthropic's report that many agents with isolated contexts outperformed a single agent, alongside the costs — up to 15× more tokens than chat, careful prompt engineering to plan sub-agent work, and coordination overhead. It also covers isolating context in an execution environment, using HuggingFace's CodeAgent running in a sandbox as the example, and isolating it in fields of a runtime state object. See [[DefinedTerm/multi-agent-orchestration]].
- **Measure first.** Before applying any of this, the post advises having a way to look at your data and track token usage, and a way to test whether a context engineering change helps or hurts.

## Context

The post is one of two widely circulated 2025 treatments of the topic that arrive at compatible but differently organised accounts; [[TechArticle/effective-context-engineering-for-ai-agents]] frames the same problem around a finite "attention budget" and groups its long-horizon techniques as compaction, structured note-taking, and multi-agent architectures. Where that piece argues from model behaviour, this one argues from a survey of what shipped agents do, and its four buckets are offered as categories for organising existing practice rather than as a claim about how models work.

Several of the strongest claims in the post are relayed from elsewhere — Cognition's assertion that context engineering is "effectively the #1 job of engineers building AI agents," Anthropic's multi-agent results, Breunig's failure modes, and the papers behind scratchpads and memories — and the post links to each rather than establishing them itself.
