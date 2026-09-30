---
title: "Agent design lessons from Claude Code"
type: "schema:BlogPosting"
lang: en
tags: [agent-architecture, agent-loop, sub-agents, context-management]
sources:
  - type: url
    url: 'https://jannesklaas.github.io/ai/2025/07/20/claude-code-agent-design.html'
    hash: sha256:4a0473d4cac9881fc7c599ead1e961497f8b69dd92f740662432f38a1d48ce18
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A July 2025 blog post by Jannes Klaas that inspects Claude Code's API traffic through a proxy to draw lessons for designing other agents. It argues that Claude Code is a relatively simple single-agent loop whose ability to stay on track comes from TODO lists, instructions embedded in tool results, system reminders and sub-agents."
  author: ["Jannes Klaas"]
  datePublished: "2025-07-20"
---

Jannes Klaas's post, dated July 20, 2025, sets out what can be learned from
[[SoftwareApplication/claude-code]] when designing one's own agents. Rather than a how-to guide, it
reports what he saw by routing Claude Code's API requests through a third-party proxy tool that
exposes the requests the agent makes, with screenshots of those requests throughout.

His central observation is that Claude Code's design is relatively simple: a standard agentic pattern
for a single agent, combined with a set of tricks for running long sessions and carefully designed
tools for editing code. He credits much of its capability to the model knowing how to use those tools
and follow a complex plan in one session, but argues that the surrounding design makes effective use
of the model, and that its simplicity is itself what lets it handle many tasks without specialised
modules.

## Key Points

- Claude Code is a single agent loop with 14 tools: four command-line tools (bash, glob, grep, ls), six
  for files (read, write, edit, multi edit, notebook read, notebook edit), two for the web (web search,
  web fetch) and two for control flow (todo write, task). The author speculates that tools were split
  out either for permission reasons — bash requires user approval while glob, grep and ls do not — or
  to handle particular file types such as Jupyter notebooks.
- It does not use a critic pattern to review its own work, does not assume different roles, has no
  sophisticated memory system and uses no databases to represent knowledge.
- Its core is a `while(tool_use)` loop: if the model's message includes a tool call, the tool runs and
  its result is fed back; if not, the loop stops and the agent waits for user input. There is no
  explicit stop tool or termination regex, so the agent can ask a clarifying question simply by
  replying in text.
- It plans with a TODO list, usually created by the very first tool call and rewritten in full on each
  update; the list also serves as a UX component showing the user where Claude is in its work.
- Tool results carry fixed instruction text appended to them — for example not to engage with
  malicious files, or, for the todo tool, to keep using the list and move on to the next task. The
  author reasons that repeating instructions on every tool use likely yields higher adherence than
  stating them only in the system prompt.
- Statically generated [[DefinedTerm/system-reminder]] blocks are attached to user messages, depending
  on the tool called and the state of the TODO list, to keep the agent on its plan across the hundreds
  of steps it often takes in one go.
- Sub-agents are dispatched through the `Task` tool for context-window management and for speed
  through parallelism. On the author's reading, a sub-agent is another instance of Claude Code with the
  same system prompt, is not told it is a sub-agent, and cannot dispatch sub-agents of its own.
- Commands the main model is about to execute are sent to Claude Haiku, which returns structured output
  listing the file paths the command reads or modifies. The author infers that Anthropic deliberately
  traded accuracy for speed here, and that these outputs are likely used to decide whether user
  approval is needed when a user chooses to allow all similar commands.

## Context

All of these findings come from the author's own inspection of one tool's request traffic rather than
from documentation, and several of the explanations — why tools were split, what the Haiku output is
used for — are stated as his inferences. He frames most of what he found as ways of keeping a single
agent on track over a long sequence of complex tasks, which lets the main agent's design stay simpler
with less need for complex scaffolding, and says the lessons carry over to other agentic designs he is
working on. The findings bear on [[DefinedTerm/sub-agent-architecture]] and
[[DefinedTerm/structured-note-taking]].
