---
title: "coding agent"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://simonw.substack.com/p/vibe-engineering'
    hash: sha256:ef207bce62b3ace1d79b606bd1e4f06b56960f2525d3a90b75215d9f9c381aa2
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://code.claude.com/docs/en/best-practices'
    hash: sha256:92807ef3d58f63fbea435ea928df49e2f3341e118eb8c40db08800c100a4c4c5
  - type: url
    url: 'https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf'
    hash: sha256:c63d41952636629543bbc11004c9be52b96f346284383c32bcd91f9130d25932
  - type: url
    url: 'https://developers.googleblog.com/en/the-next-chapter-of-the-gemini-era-for-developers/'
    hash: sha256:14b103534d56b72c11ed40d81d382de5a7a3e724fdc4de1f2a18de4524165941
  - type: url
    url: 'https://blog.google/innovation-and-ai/models-and-research/google-labs/jules/'
    hash: sha256:600f7a1ec8134e15607bb66edb2851d78e361864e2e6017d9ccec7914744aafc
  - type: url
    url: 'https://openai.com/index/introducing-codex/'
    hash: sha256:c899f94e6c00781777e4a0c930a154bee0271654282a1a6f195b368868a1366b
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A tool that iterates on code — actively testing and modifying it until it achieves a specified goal — rather than returning a single response to a prompt; an instance of the more general definition of an agent as an LLM calling tools in a loop toward a goal."
---

A coding agent is a tool that iterates on code, actively testing and modifying it until it achieves a specified goal, rather than returning a single response and stopping. [[Person/simon-willison]] gives that characterisation in [[BlogPosting/vibe-engineering]], naming Claude Code (released February 2025), OpenAI's Codex CLI (April) and Gemini CLI (June) as examples, and credits their rise with dramatically increasing the usefulness of LLMs for real-world coding problems. It is a special case of the general definition he has settled on for agents — LLMs calling tools in a loop to achieve a goal — a definition Anthropic's engineering writing independently converges on, phrasing it as LLMs autonomously using tools in a loop.

## Usage

The distinguishing property is the loop, not the interface. Anthropic's Claude Code documentation makes the same contrast in product terms: unlike a chatbot that answers questions and waits, an agentic coding environment can read files, run commands, make changes, and work through problems autonomously while the user watches, redirects, or steps away — which is what changes how the work is organised, since the human describes what they want rather than writing the code and asking for review.

Anthropic's [[TechArticle/effective-context-engineering-for-ai-agents]] adds that autonomy scales with model capability: as the underlying models become more capable, the level of autonomy of agents can scale, letting them independently navigate nuanced problem spaces and recover from errors. Willison reports experienced engineers running multiple copies of agents at once to tackle several problems in parallel, something he says he was initially skeptical of and now does himself, describing it as surprisingly effective if mentally exhausting.

Practitioner writing distinguishes coding agents from earlier AI coding tools along a spectrum. Anthropic's [[Report/2026-agentic-coding-trends-report]] describes the progression by task horizon: early agents handled one-shot tasks taking a few minutes — fix this bug, write this function, generate this test — while by late 2025 agents were producing full feature sets over several hours, with the report predicting work spanning days in 2026.

### The asynchronous turn

A second axis, distinct from the loop, is whether the developer waits. Two vendors announced cloud-hosted agents in the same period whose defining property is that the developer does not: [[Organization/openai]] launched [[SoftwareApplication/codex]] on 16 May 2025 as "a cloud-based software engineering agent that can work on many tasks in parallel", each task running in its own isolated sandbox preloaded with the repository, and Google Labs took [[SoftwareApplication/jules]] to public beta on 20 May 2025 as an agent that clones the codebase into a cloud VM and "operates asynchronously, allowing you to focus on other tasks while it works in the background."

Both vendors describe the same requirement that asynchrony forces: evidence of what the agent did, and a human review step before anything lands. Google's Jules "presents its plan, reasoning and a diff of the changes made" and lets the developer modify the plan before, during and after execution — an inspectable plan OpenAI's Codex did not have at launch, which listed mid-task course correction among the features it lacked and interactive collaboration among its future plans. What Codex supplied instead was traceability after the fact: it commits its changes in its own environment and provides "verifiable evidence of its actions through citations of terminal logs and test outputs", with progress monitorable in real time, while insisting it "remains essential for users to manually review and validate all agent-generated code before integration and execution."

Each frames this as a shift in how work is organised rather than a feature. OpenAI predicted that "the asynchronous, multi-agent workflow introduced by Codex in ChatGPT will become the de facto way engineers produce high-quality code", and that real-time pairing and task delegation would ultimately converge into one workflow; Google's framing was that "agentic development is shifting from prototype to product and quickly becoming central to how software gets built." Both are vendor predictions about their own products, made at launch, not observed outcomes — and OpenAI conceded in the same post that delegating to a remote agent takes longer than interactive editing and "can take some getting used to".

Google's earlier post introducing Jules, of December 2024, also records what it was measuring against. It reported 51.8% on [[Dataset/swe-bench]] Verified from research using Gemini 2.0 Flash equipped with code execution tools, attributing the result partly to inference speed letting the agent sample hundreds of potential solutions and select the best using existing unit tests and the model's own judgment, and said it was in the process of turning that research into developer products. OpenAI's Codex post states no SWE-bench score of its own, only the configuration it used.

## Related Terms

The mode of working built on these tools is [[DefinedTerm/agentic-coding]], and the practices for doing so accountably are covered under [[DefinedTerm/vibe-engineering]] and [[DefinedTerm/agentic-engineering]]. Their central engineering constraint is [[DefinedTerm/context-engineering]]; the runtime that wraps the loop is covered under [[DefinedTerm/agent-harness]]. Named examples with their own pages include [[SoftwareApplication/claude-code]], [[SoftwareApplication/codex-cli]], [[SoftwareApplication/gemini-cli]], [[SoftwareApplication/cursor]], and [[SoftwareApplication/kiro]].
