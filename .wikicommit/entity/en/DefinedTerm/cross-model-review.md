---
title: "Cross-model review"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, agentic-code-review, coding-agents]
sources:
  - type: url
    url: 'https://note.com/hacklog_stealth/n/n395c7ca5da82'
    hash: sha256:3e5e8c433b66bc4010afcf256d50e5070473d9728c98a9c9f8174b40a3bb1162
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "The practice of having AI-generated code reviewed by a different model from the one that wrote it, rather than asking the implementing model to review its own work, so that the reviewer does not share the implementer's unstated assumptions."
---

Cross-model review is the practice of assigning the review of AI-written code to a different model from the one that implemented it, instead of having the implementing model review its own output. The reasoning given for it in [[BlogPosting/claude-code-self-review-vs-separate-reviewer-model]] is that same-model self-review inherits the implementer's assumptions: whatever the model took for granted while writing the code — that an input exists, that a file is present — it takes for granted again while reading it, so those premises are never questioned. Prompting the same model to review "adversarially" is argued to change only its posture, not those assumptions, whereas a different model does not share them and so asks the questions the implementer never did.

## Usage

In the arrangement that post describes, implementation stays with [[SoftwareApplication/claude-code]] and only the review is handed to [[SoftwareApplication/openai-codex]]. The change under review is exported as a `git diff`, and the reviewing model is given a narrowed brief: ignore naming and formatting, and look only for implicit assumptions that can break, behaviour on edge cases such as empty, null, boundary or concurrent input, and places where errors are swallowed. Its findings are then returned to the implementing agent to fix, with the suggestion that the implementer first check each finding is actually correct, filtering out mistaken ones.

## When It Applies

It applies where one model is already writing the code and the review step is being done by that same model. It assumes access to a second model that can read the change — in the account above, nothing more than a diff and a prompt — and a way to carry findings back to the implementer. The failure it targets is assumption-level defects rather than style: the defects the post reports surfacing were a crash on first run when a config file did not yet exist, partially failed asynchronous work reported as success, and an error caught and discarded without logging. The practice rests on a single author's report from their own projects; the post gives no measurement of how often the second model's findings were right, and itself recommends verifying findings before acting on them.

## Related Terms

- [[DefinedTerm/agentic-code-review]]
- [[DefinedTerm/critical-dialogue-review]]
- [[DefinedTerm/llm-as-a-judge]]
