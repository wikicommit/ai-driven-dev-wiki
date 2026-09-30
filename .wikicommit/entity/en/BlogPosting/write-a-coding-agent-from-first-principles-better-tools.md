---
title: "Write a coding agent from first principles: better tools"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, tool-use, agent-tooling, python]
sources:
  - type: url
    url: 'https://mathspp.com/blog/write-a-coding-agent-from-first-principles-better-tools'
    hash: sha256:a1984116f7e1602a9a51a47561da2c3f8d48ea9ec9fd990feb94e38f995739c4
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A mathspp tutorial, the second part of a series on building a coding agent in Python from first principles, that replaces the agent's hand-written file-editing and shell tools with Anthropic's text editor tool and bash tool and adds guardrails around them."
  datePublished: "2026-07-06"
  publisher: "mathspp"
---

This tutorial builds on an earlier mathspp tutorial in which the reader implements a minimal coding agent with its own `bash`, `read`, `write`, `replace` and `insert` tools. Here those tools are swapped for two tools that Anthropic provides: the text editor tool, which covers the four file-editing tools in one, and the bash tool, which gives the agent a persistent shell session. The tools still run on the client side, so the agent still receives tool-use blocks in API responses, but the developer no longer writes a schema for them — they are declared only by their Anthropic type and name. The post's argument for the switch is that Anthropic trains its models on these specific tool schemas, so the agent makes better tool calls more consistently. This is the same category the wiki describes as Anthropic-schema client tools in [[DefinedTerm/client-and-server-tools]].

The tutorial is structured as a series of timed exercises, each linked to a checkpoint in a companion GitHub repository, followed by a worked solution. It ends with an agent of roughly 300 lines of Python: about 100 for the agentic loop and command management, 100 for the text editor tool and 100 for the bash session and its manager.

## Key Points

- The text editor tool is declared with the name `str_replace_based_edit_tool` and the type `text_editor_20250728`; the post notes that the type's date suffix is a version that may influence the tool's behaviour.
- Each text-editor request carries a `command` field, and the tutorial dispatches on it to four functions — `create`, `str_replace`, `view` and `insert` — wrapping the dispatch in a single exception handler so that errors such as a missing permission are handled in one place.
- For `str_replace`, the tutorial advises a plain string replacement rather than regular expressions, since the model supplies a literal string, and following the documentation it rejects the edit unless the old text occurs exactly once.
- `view` has to handle both files and directories and an optional 1-based `view_range` in which `-1` means "to the end of the file"; splitting with `splitlines(keepends=True)` is used to preserve newline characters, a detail that matters again for `insert`.
- The post suggests restricting `create`, `str_replace` and `insert` to the current working directory and backing a file up with a timestamped copy before each edit, and shows that the order of the two decorators matters: the directory check must run first, or a rejected edit outside the working directory still leaves a stray backup behind.
- The bash tool is declared with the name `bash` and the type `bash_20250124`. Its main difficulty is persistence, which the tutorial implements as a bash subprocess with piped input and output, a daemon thread that feeds output lines into a queue, and a sentinel `echo __DONE__` sent after each command so the reader knows when the command's output has ended.
- Timeouts are enforced by reading from the queue with a timeout computed from the time remaining; the tool also handles a `restart` request by closing the session and starting a new one.
- Following a recommendation in Anthropic's documentation, very long outputs are truncated — but only after all output up to the sentinel has been read, since stopping early would let the rest of one command's output be mistaken for the next command's; a note is appended telling the model it did not see everything.
- Because a bash tool gives the agent full control of the machine, the tutorial adds a guardrail that asks the user to approve each command once, always, or not at all, and informs the agent when a command is refused. It warns that approving by executable name rather than full command must account for pipes and chained commands, so that approving `ls` does not also approve `ls && …` followed by arbitrary code.

## Context

The post is a hands-on teaching piece rather than an argument about agent design; its claims about why Anthropic's tools work better rest on Anthropic's own description of how its models are trained, and it cites Anthropic's tool reference, text editor tool and bash tool documentation as its references. It suggests follow-up work of response streaming, a richer terminal interface, in-session user commands such as resetting context or switching models, and wrapping the agent in a CLI as a step toward subagents.
