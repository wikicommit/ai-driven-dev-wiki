---
title: "How and when to build multi-agent systems"
type: "schema:BlogPosting"
lang: en
tags: [agents, multi-agent-systems, context-engineering]
sources:
  - type: url
    url: 'https://www.langchain.com/blog/how-and-when-to-build-multi-agent-systems'
    hash: sha256:e483f00bb47465df271140cec29e7582c51eba2135ad16725c2552799d81317f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A June 2025 LangChain blog post reading Cognition's \"Don't Build Multi-Agents\" and Anthropic's account of its multi-agent research system side by side, and arguing that despite their opposing titles they agree that context engineering is crucial and that multi-agent systems which mainly read are easier to build than ones that write."
  author: ["Harrison Chase"]
  datePublished: "2025-06-16"
  publisher: "LangChain"
---

*How and when to build multi-agent systems* is a LangChain blog post written in response to two posts
released late the previous week with seemingly opposite titles: [[BlogPosting/dont-build-multi-agents]] from
[[Organization/cognition]] and [[BlogPosting/how-we-built-our-multi-agent-research-system]] from
[[Organization/anthropic]]. The author argues that the two have a lot in common, and draws from them two
insights into how and when to build multi-agent systems: context engineering is crucial, and systems that
primarily "read" are easier to build than those that "write".

The post then turns to reliability and engineering challenges that it says arise whether one builds a
multi-agent system or a complex single agent — durable execution, debugging and observability, and
evaluation — and connects each to LangChain's own tooling. It concludes that there is no one-size-fits-all
answer, and that the right point on the spectrum between single and multiple agents depends on the
problem being solved.

## Key Points

- The post credits the Cognition post with introducing the term [[DefinedTerm/context-engineering]] for
  the challenge of communicating to models the context of what they are being asked to do, and reads the
  Anthropic post as addressing the same issue at several points without using the term.
- It draws from the Cognition post that multi-agent systems make it harder to ensure each sub-agent has
  the appropriate context.
- Read actions are, in its argument, inherently more parallelizable than write actions: parallel writing
  requires both communicating context between agents and merging their outputs, and conflicting writes
  produce far worse results than conflicting reads.
- It cites Anthropic's research system as an illustration: multiple agents handle the research, while the
  final report is written by a single main agent in one call. It adds that even read-heavy systems still
  need careful context engineering.
- It presents durable execution, agent debugging and observability, and agent evaluation as generic
  problems for long-running agents rather than ones specific to Anthropic's use case, and argues that
  durable execution should be built into the agent orchestration framework.
- It picks out three evaluation takeaways from the Anthropic post: start small, with around 20 datapoints
  being enough; [[DefinedTerm/llm-as-a-judge]] can automate scoring; and human testing remains essential.
- Its own recommendation is that an agent framework should let developers "slide anywhere" between single
  and multiple agents, which it says LangGraph uniquely emphasizes — a claim the author, whose company
  builds that framework, makes about his own product.

## Context

The post is a commentary on two other companies' writing rather than an account of its own experiments,
and most of its evidence is quoted from the Anthropic and Cognition posts. It is written from the
perspective of the maker of [[SoftwareApplication/langgraph]] and LangSmith, and each engineering
challenge it discusses ends with how those products address it: it describes LangGraph as a low-level
orchestration framework with no hidden prompts and no enforced "cognitive architectures", giving full
control over what is passed to the LLM, and LangSmith as its platform for agent debugging, observability
and evaluation.
