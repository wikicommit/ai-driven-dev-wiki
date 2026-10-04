---
title: "Agent 编程方法论：不教工具教方法，让 AI 按你的规矩干活"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, context-engineering, coding-agents, claude-code]
sources:
  - type: url
    url: 'https://xiangyugongzuoliu.com/agent-programming-methodology-guide/'
    hash: sha256:bd701fb9688b450657450c73dcd5e17c6f19510d2ca852bc1907a9c9c4ecfc43
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A June 2026 Chinese-language guide by the AI-programming blogger Xiangyu that gathers ten tutorials into an \"agent programming methodology\". It argues that methods for making a coding agent work by your project's rules outlast any particular tool, with harness engineering as the overarching framework and context engineering, project memory, prompting, thinking frameworks, runtime control and extension mechanisms beneath it."
  author: ["翔宇 (Xiangyu)"]
  datePublished: "2026-06-06"
---

This guide, written in Chinese by the AI-programming blogger Xiangyu (翔宇), is an overview page that
links ten of the author's in-depth tutorials, most of them about [[SoftwareApplication/claude-code]].
Its premise is in its title: rather than teaching how to operate a tool, it teaches methods for making an
agent do its work by your rules. Tools turn over every half year, the author writes — last year Cursor,
this year mainly Claude Code and Codex — but the methods for controlling an agent carry over, so someone
who has learned the methodology only has to adapt to a new tool's interface.

The author argues that most people stop at knowing how to use a tool, and on complex projects find that
agents drift off course, forget things, overstep their authority or make unexpected judgments at key
steps. In his view the problem is not the tool but the absence of rules set for the agent. The guide
answers one question — how to make an agent work reliably in your project — and ends with a
self-assessment checklist and a table recommending which tutorials to read for which pain point.

## Key Points

- The author distinguishes three concepts he says are often confused. [[DefinedTerm/prompt-engineering]]
  concerns how to write instructions for a single exchange. [[DefinedTerm/context-engineering]], which
  he attributes to Shopify CEO Tobi Lutke, concerns feeding the agent the right information at the right
  time. [[DefinedTerm/harness-engineering]] he describes as the overarching framework he has summarised
  from his own practice: managing the agent like a new employee through rule files, context strategy,
  permission boundaries and extension mechanisms. In his framing the three are nested rather than
  alternatives, with the first two as sub-dimensions of harness engineering.
- He gives harness engineering a four-layer architecture that works together: a rules layer (project
  memory such as [[DefinedTerm/claude-md]]), an information layer (context engineering), an instruction
  layer (prompt engineering) and a boundary layer (runtime control through permissions and sandboxes).
  Its core challenge, he argues, is constraining an executor that makes its own judgments, so what one
  writes are criteria for judgment rather than execution steps.
- He sums up context engineering as feeding the right information, at the right time, in the right
  format, and sorts injection methods by how long the information stays valid: permanent information
  in a project memory file, session-level information in the system prompt or first message, on-demand
  information through tool calls and retrieval, and real-time information from execution results. He
  warns against equating context engineering with RAG, which he treats as only one of its techniques.
- He presents project memory files — `CLAUDE.md` for Claude Code, [[DefinedTerm/agents-md]] for OpenAI
  Codex, `.cursorrules` for Cursor — as the persistent carrier of rules for an agent that is otherwise
  stateless, highlights CLAUDE.md's global, project and directory levels, and advises writing
  behavioural constraints and decision preferences rather than encyclopaedic knowledge or operating
  steps, iterating on the file whenever the agent makes an unwanted judgment, and putting hard red lines
  near the top because agents attend more to the beginning and end.
- For prompts in agent programming he recommends explicit constraint boundaries, decomposition into
  independently verifiable steps and predefined criteria for done, and suggests that showing an example
  file works better than describing a desired style.
- He argues that specifying a thinking framework (first principles, inversion, MECE, 5-Why and the
  like), per session or fixed in the project memory file, matters less for making the agent smarter
  than for making its analysis predictable and reproducible.
- Runtime control, in his account, has three dimensions: managing the context window (including
  automatic compaction), choosing a thinking mode by the length of the task's reasoning chain, and
  configuring permissions on the principle of least privilege, loosened gradually as trust grows but
  kept conservative in production. Extension mechanisms add [[DefinedTerm/agent-hooks]] as runtime
  checkpoints for automated safety and quality checks, and plugins as a standard way to give the agent
  new capabilities.
- He predicts that agent programming methodology will become a basic skill for every technical person,
  like version control and automated testing.

## Context

The guide is a practitioner's synthesis, which also points readers to the author's course, rather than a report of
measurements; much of its detail concerns Claude Code's features as the author describes them, while
its claim is that the methods themselves are tool-independent. Its own use of "harness engineering" as
an umbrella over context and prompt engineering is the author's framing.
