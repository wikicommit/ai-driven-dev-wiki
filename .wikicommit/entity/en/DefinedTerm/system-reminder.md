---
title: "System Reminder"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, context-management, prompt-engineering]
sources:
  - type: url
    url: 'https://jannesklaas.github.io/ai/2025/07/20/claude-code-agent-design.html'
    hash: sha256:4a0473d4cac9881fc7c599ead1e961497f8b69dd92f740662432f38a1d48ce18
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A block of fixed instruction text, wrapped in a system-reminder tag, that Claude Code attaches to user messages to keep the agent on its instructions and plan over long sessions, as observed by Jannes Klaas in a July 2025 blog post."
---

A system reminder is a block of text wrapped in a `<system-reminder>` tag that
[[SoftwareApplication/claude-code]] attaches to the user message during a session, as observed in
[[BlogPosting/agent-design-lessons-from-claude-code]]. According to that post, the reminders are
generated statically, depending on the tool that was just called and on the state of the agent's TODO
list, and they exist to counter an agent forgetting its instructions or plan after many steps.

## Usage

The post describes three kinds of reminder seen in Claude Code's API requests: one at the beginning of
the conversation restating general instructions (such as doing only what was asked and not creating
files unless necessary), noting that the context may or may not be relevant; one after the first user
message noting that the todo list is empty and suggesting the TodoWrite tool if the task would benefit
from it, with an instruction not to mention the reminder to the user; and one attached after various
steps giving the latest contents of the todo list and telling the agent to continue with the tasks at
hand. The author presents them alongside a related technique — fixed instruction text appended to tool
results — and reasons that repeating instructions in this way likely produces higher adherence than
placing them only in the system prompt. He regards periodic reminders of the main control flow as
important because Claude Code frequently takes hundreds of steps in one go.

## Related Terms

- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/claude-md]]
