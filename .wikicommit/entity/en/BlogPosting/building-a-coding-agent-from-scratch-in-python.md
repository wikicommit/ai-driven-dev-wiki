---
title: "Pythonでゼロから作るコーディングエージェント"
type: "schema:BlogPosting"
lang: en
tags: [multi-agent-systems, coding-agents, tool-use, agent-frameworks]
sources:
  - type: url
    url: 'https://zenn.dev/finatext/articles/create-codingagent-from-scratch'
    hash: sha256:f2f67945e5431dbe4a2a268e3e16b3b5db6f49d349699e7530f7ec02476812bc
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A Nowcast data engineer's account of building a multi-agent coding agent from scratch in Python with LangChain and Azure OpenAI GPT-4.1, in which a programmer agent and a reviewer agent iterate under a coordinator until the reviewer approves."
  author: "Takumi"
  datePublished: "2025-06-17"
  publisher: "Finatext Tech Blog"
---

This post walks through a coding agent built from scratch for an internal generative-AI contest in the Finatext group. The full contest system took a request sent over Slack through code writing, review and pull-request creation on GitHub; the post narrows its scope to the coding part, a multi-agent arrangement the author calls the Coordinator. It is written as an implementation walkthrough, using [[SoftwareApplication/langchain]] and Azure OpenAI GPT-4.1, and the code is published in a public repository.

The design separates generation from review. A ProgrammerAgent writes code using file and Git tools, a ReviewerAgent judges the resulting diff, and an AgentCoordinator runs them in a loop, feeding the reviewer's comments back to the programmer until the reviewer records approval or an iteration limit is reached. The post is a concrete instance of the generate-and-review pattern discussed on [[DefinedTerm/llm-based-multi-agent-system]] and [[DefinedTerm/code-review-agent]].

## Key Points

- The system has three parts: a ProgrammerAgent that generates code from the user's instruction, a ReviewerAgent that reviews the generated code, and an AgentCoordinator that manages the cycle between them.
- The ProgrammerAgent's tools cover listing, reading, creating and overwriting files, web search and opening URLs, creating a Git branch and generating a diff.
- The ReviewerAgent's tools are a code-review tool, a tool that records an LGTM, and a tool that runs unit tests with pytest. Its system prompt asks it to review for code quality, security, best-practice compliance, potential bugs and design issues, and to call the LGTM tool when the code can be approved.
- The code-review tool does no processing itself: it returns a stub, and the review content is produced by the LLM through function calling.
- The coordinator can create a working branch first, then alternates programmer and reviewer for up to a maximum number of iterations (three in the code shown), passing the reviewer's summary to the next programmer run and stopping early once LGTM is recorded.
- Tools are defined as LangChain structured tools (see [[DefinedTerm/structured-tool]]), each with a Pydantic input schema; the project derives them from a common base class so that every tool has the same shape.
- The author chose GPT-4.1 after trying GPT-4o, GPT-4o mini and o3, because the task needed roughly 220,000 tokens — beyond the 128K limit of 4o and 4o mini — and because generating several files at once needed a large context window. The author ties this to the contest's target being Terraform with many reference documents, and expects other models, including Gemini and Claude, to be adequate for simpler code generation.
- An example run asked for a user-management API with FastAPI, and produced a set of files (authentication, CRUD, database, exceptions, models and schemas) after the reviewer recorded LGTM.

## Context

The author's closing reflection is that building a coding agent from zero made the polish of existing tools such as [[SoftwareApplication/cursor]] more apparent. Stated next steps are serving the agent as a web API, indexing the reference documents to reduce the cost of reading them, and abstracting the LLM client so that models other than GPT-4.1 can be used. None of these are reported as done.
