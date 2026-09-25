---
title: "Agentic Design Patterns Part 3, Tool Use"
type: "schema:BlogPosting"
lang: en
tags: [agents, tool-use, agent-architecture, agentic-design-patterns]
sources:
  - type: url
    url: 'https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-3-tool-use'
    hash: sha256:f6402a3fe89e2e1e8e08eb769fbf3dc97994f6b04e1f57f8702632cabc6b897b
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A letter in DeepLearning.AI's The Batch, third in a series on agentic design patterns, describing Tool Use — giving an LLM functions it can request to call — as a key design pattern of AI agentic workflows."
  author: ["Andrew"]
  datePublished: "2024-04-03"
  publisher: "DeepLearning.AI"
---

This short letter, published in The Batch and signed "Andrew", is the third in a series on agentic design patterns. It defines Tool Use ([[DefinedTerm/tool-use-design-pattern]]) as the pattern in which an LLM is given functions it can request to call for gathering information, taking action or manipulating data, and calls it a key design pattern of AI agentic workflows — one that, it says, goes well beyond the web search and code execution that some large consumer-facing LLMs already incorporate.

The letter explains the mechanism through two examples. Asked which coffee maker reviewers rate best, an LLM might decide to run a web search: it is fine-tuned or prompted, perhaps with few-shot prompting, to generate a special string requesting a call to a search engine, and a post-processing step detects that string, calls the search function with the relevant parameters, and passes the result back to the LLM as additional context. Asked what $100 at 7% compound interest grows to after 12 years, it might instead use a code-execution tool to run a Python expression rather than generate the answer directly with a transformer network, which the letter says is unlikely to give the right answer.

## Key Points

- Early on, according to the letter, LLM developers realised that relying only on a pre-trained transformer to generate output tokens is limiting, and that giving an LLM a web-search tool lets it do much more.
- The letter states that the exact format of a tool-request string depends on the implementation.
- Developers, it says, now use functions to search different sources, interface with productivity tools such as email and calendars, and generate or interpret images; an LLM can be prompted with detailed descriptions of many functions — what each does and what arguments it expects — and is expected to choose the right one for a job.
- Where an LLM has access to hundreds of tools, too many to fit in its context, the letter says heuristics may be used to pick the most relevant subset for the current step, and likens this to how retrieval augmented generation systems pick a subset of text to include.
- It notes that before large multimodal models were widely available, LLMs could not process images directly, so much early tool-use work came from the computer vision community, where calling a function such as object recognition was the only way for an LLM-based system to manipulate an image.
- It calls GPT-4's function calling capability, released in the middle of the year before the letter, a significant step toward a general-purpose implementation, and says more and more LLMs have since been developed to be similarly facile with tool use.

## Context

The letter recommends three research papers for readers who want to learn more about tool use. It places Tool Use alongside Reflection, covered in the previous letter of the series, as design patterns the author can get to work fairly reliably in his applications, and announces that later letters will describe the Planning and Multi-agent collaboration patterns, which it describes as allowing AI agents to do much more but as less mature and less predictable.
