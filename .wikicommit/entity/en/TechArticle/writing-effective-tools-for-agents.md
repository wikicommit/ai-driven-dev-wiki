---
title: "Writing effective tools for agents — with agents"
type: "schema:TechArticle"
lang: en
tags: [agentic-coding, context-engineering, mcp, agent-architecture]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/writing-tools-for-agents'
    hash: sha256:effc06d088266ee895582c23541e543435288246b1dc4d89d3a2f4b8a1993b54
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Anthropic's engineering post on designing tools for agents rather than for other software: how to prototype and evaluate tools, how to have Claude optimize its own tools against that evaluation, and five principles for tool design centred on the agent's limited context."
  author: "Ken Aizawa"
  datePublished: "2025-09-11"
  publisher: "[[Organization/anthropic]]"
---

"Writing effective tools for agents — with agents" is an Engineering at Anthropic post of 11 September 2025 by Ken Aizawa. Its argument is that a tool is a new kind of software — "a contract between deterministic systems and non-deterministic agents" — and that writing one therefore cannot be approached the way a function or API for another developer would be. Its practical proposal is an evaluation-driven loop in which agents are used to improve the tools those same agents will use.

## Key Points

The post's framing distinction is between traditional software, where `getWeather("NYC")` always behaves identically, and an agent, which given "Should I bring an umbrella today?" might call the weather tool, answer from general knowledge, ask a clarifying question, or fail to grasp the tool at all. Its stated goal is to increase the surface area over which agents can be effective, and it observes that in its experience the tools most "ergonomic" for agents are also surprisingly intuitive for humans.

The workflow it describes has three stages. **Prototype** the tools and test them by hand — wrapping them in a local MCP server or a Desktop extension so they can be exercised in Claude Code or the Claude Desktop app, and giving Claude the relevant library, API or SDK documentation when having it write the tools. **Evaluate** by generating many tasks grounded in real-world use, each paired with a verifiable outcome; the post is specific that weak tasks are single-step lookups ("Search the payment logs for `purchase_complete` and `customer_id=9182`") while strong ones may require dozens of tool calls ("Customer ID 9182 reported that they were charged three times for a single purchase attempt. Find all relevant log entries and determine if any other customers were affected by the same issue."). **Collaborate** by concatenating the evaluation agents' transcripts and pasting them into Claude Code to analyse results and refactor tools.

On analysis it makes a point that generalises past tool design: what agents omit from their feedback is often more important than what they include, because LLMs "don't always say what they mean" — so raw transcripts must be read alongside the agents' stated reasoning. Its worked example of a defect found this way is Claude needlessly appending `2025` to the `query` parameter of the web search tool at launch, which biased results and was corrected by improving the tool description.

The five principles it distils are:

- **Choose the right tools.** More tools do not always lead to better outcomes, and a common error the post reports observing is tools that merely wrap existing software functionality or API endpoints regardless of whether they suit an agent. Because an agent's context is limited where computer memory is cheap, a tool returning all contacts forces brute-force reading; the post recommends `search_contacts` or `message_contact` over `list_contacts`, and consolidating chained operations into one call — `schedule_event` instead of `list_users`/`list_events`/`create_event`, `search_logs` instead of `read_logs`, `get_customer_context` instead of three separate customer lookups.
- **Namespace them.** Grouping related tools under common prefixes by service (`asana_search`, `jira_search`) and by resource (`asana_projects_search`, `asana_users_search`) can help agents select the right tools at the right time among the potentially hundreds available. The post reports that prefix- versus suffix-based namespacing has non-trivial and model-dependent effects on its own tool-use evaluations.
- **Return meaningful context.** Tools should return high-signal information and avoid low-level identifiers such as `uuid`, `256px_image_url` and `mime_type` in favour of `name`, `image_url` and `file_type`. The post reports that resolving arbitrary alphanumeric UUIDs into semantically meaningful language, or even a 0-indexed ID scheme, significantly improves Claude's precision in retrieval tasks by reducing hallucinations. Where both forms are needed it suggests a `response_format` enum letting the agent request `"concise"` or `"detailed"` responses, and reports its Slack example using roughly a third of the tokens in concise form.
- **Optimize for token efficiency.** Pagination, range selection, filtering and truncation with sensible defaults are recommended for any response that could consume large amounts of context; the post states that Claude Code restricts tool responses to 25,000 tokens by default. Truncation and error messages are themselves treated as prompts: an error should communicate specific, actionable improvements rather than opaque codes or tracebacks.
- **Prompt-engineer the descriptions.** The post calls this one of the most effective methods available, advising authors to describe a tool as they would to a new hire — making implicit context such as specialized query formats and niche terminology explicit — and to name parameters unambiguously (`user_id`, not `user`). Its cited evidence is its own: that Claude Sonnet 3.5 achieved state-of-the-art performance on [[Dataset/swe-bench]] Verified after precise refinements to tool descriptions.

## Context

The post presents its advice as derived rather than theorised: it states that most of it came from repeatedly optimizing Anthropic's internal tool implementations with Claude Code, with evaluations built on the company's own internal workspace, and that held-out test sets showed further gains beyond "expert" implementations written either by its researchers or by Claude. Its closing position is that building tools for agents requires re-orienting software development practice from deterministic patterns to non-deterministic ones, and that effective tools are "intentionally and clearly defined, use agent context judiciously, can be combined together in diverse workflows, and enable agents to intuitively solve real-world tasks".

Its claims about the performance of its own tools and models are Anthropic's own, published about its own products, with no independent verification. Because the argument throughout is about spending an agent's limited context well, it sits alongside the company's other writing on [[DefinedTerm/context-engineering]] rather than apart from it, and treats [[DefinedTerm/model-context-protocol]] as the delivery mechanism whose scale — potentially hundreds of tools — creates the problem it addresses.
