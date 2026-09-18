---
title: "Claude Code"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, anthropic, coding-tools, context-window]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Anthropic's agentic coding solution, which combines up-front context files with just-in-time file and data retrieval, message-history compaction, and to-do list note-taking."
  applicationCategory: "Agentic coding tool"
  featureList: "Targeted database queries with stored results; Bash primitives including head, tail, glob and grep; CLAUDE.md context files loaded up front; message-history compaction; a to-do list for agentic note-taking"
  author: "[[Organization/anthropic]]"
---

Claude Code is Anthropic's agentic coding solution. Anthropic uses it as the worked example for
several of the [[DefinedTerm/context-engineering]] techniques it recommends, and describes it as
performing complex data analysis over large databases without ever loading full data objects into
context: the model writes targeted queries, stores the results, and leverages Bash commands such
as `head` and `tail` to analyse large volumes of data.

Anthropic characterises Claude Code as employing a hybrid context strategy — retrieving some data
up front for speed while pursuing further autonomous exploration at its discretion. CLAUDE.md
files are naively dropped into context up front, while primitives such as glob and grep let it
navigate its environment and retrieve files just in time, which Anthropic says effectively
bypasses the issues of stale indexing and complex syntax trees.

## Capabilities
- [[DefinedTerm/just-in-time-context-retrieval]] over large data sets: targeted queries whose
  results are stored, plus Bash primitives such as `head` and `tail` for working through large
  volumes without loading them whole.
- File-system navigation through glob and grep, retrieving files as they are needed rather than
  from a pre-built index.
- CLAUDE.md files, dropped into context up front as the fixed half of its hybrid strategy.
- [[DefinedTerm/compaction]] of the message history: the history is passed to the model to
  summarise and compress the most critical details, preserving architectural decisions,
  unresolved bugs and implementation details while discarding redundant tool outputs or messages.
  The agent then continues with that compressed context plus the five most recently accessed
  files, which Anthropic says gives users continuity without their having to worry about context
  window limitations.
- A to-do list, which Anthropic gives as an instance of [[DefinedTerm/structured-note-taking]].
- An on-demand planning mode, added more recently than some rival agents, in which the agent generates a plan and awaits human review before proceeding — contrasted by [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] with Google's [[SoftwareApplication/google-jules]], which has included a planning step from its inception.

## Adoption & Ecosystem

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] describes Claude Code's architecture as having shifted from a monolithic agent to a multi-agent one, spawning specialized sub-agents for specific tasks. The same paper cites it as an example of a powerful command-line agentic platform that grants developers immense control and flexibility but results in ephemeral interactions: the conversational context of planning, clarification, and refinement between the human and the agent exists only in a terminal's scroll-back buffer, with no systematic archival of the agent's reasoning or the human's guidance, making it difficult to reconstruct the evolution of design decisions or reproduce specific outcomes.
