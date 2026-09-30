---
title: "Shadow Workspace"
type: "schema:DefinedTerm"
lang: en
tags: [ai-ide, coding-agents, lsp]
sources:
  - type: url
    url: 'https://aise.phodal.com/agent-for-aise.html'
    hash: sha256:25e468d7ba5ae035373a0284184294acc7158b0787c0e16b94a2c358beceec39
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A hidden, separate editor window in which Cursor applies an AI's proposed edits in the background, so that the AI can receive lint feedback from the language server and iterate on its code without affecting the user's own coding experience."
---

A shadow workspace is a hidden editor window, independent of the user's own, into which
[[SoftwareApplication/cursor]] applies edits an AI proposes so that the AI can see the consequences of
those edits — above all the lint diagnostics a language server reports — and decide how to iterate,
while the user keeps working undisturbed. The mechanism lets code be iterated on in the background:
the AI edits, the hidden window reports back, and the AI revises.

## Usage

Cursor's design criteria for the shadow workspace set out two goals. The first is LSP usability: the
AI should see the lints produced by its changes, be able to jump to definitions, and more broadly
interact with every part of the Language Server Protocol. The second is runnability: the AI should be
able to run its code and see the output. The design focused on LSP usability first.

Six requirements constrain how those goals are met. The user's coding experience must be unaffected
(independence); the user's code must stay safe, for example by being kept entirely local (privacy);
several AIs should be able to work at the same time (concurrency); the approach should work for every
language and every workspace setup (universality); the code should be as small and as easy to isolate
as possible (maintainability); and there should be no minute-long delays anywhere, with enough
throughput to support hundreds of AI branches (speed). Cursor explains that many of these reflect the
reality of building a code editor for more than a hundred thousand users whose experience it does not
want to harm.

The implementation runs in four steps. The AI proposes an edit to a file; the edit travels from the
normal window's renderer process to its extension host, then to the shadow window's extension host,
and finally to the shadow window's renderer process; the edit is applied in the shadow window, which
is hidden from and independent of the user, and every lint is sent back the same way; and the AI
receives the lints and decides how to iterate. The interface between the two sides is a small RPC
service whose central call returns the lints for a change, computed as the delta between a file's
initial and final content — by default only lints that the change introduced, not ones already
present — optionally with quick fixes attached.

## Related Terms

- [[DefinedTerm/ai-ide]] — the kind of environment in which the mechanism runs
