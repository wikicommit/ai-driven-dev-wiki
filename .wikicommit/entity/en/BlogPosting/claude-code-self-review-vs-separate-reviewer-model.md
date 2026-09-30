---
title: "Claude Codeの自己レビューを信じてた。レビュー役だけ別モデルにしたら、見逃してたバグが出てきた"
type: "schema:BlogPosting"
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
  description: "A Japanese note post by the pseudonymous author Hack-Log reporting that assigning only the review step to a different model (Codex) instead of having Claude Code review its own code surfaced bugs that same-model self-review had repeatedly passed."
  author: ["Hack-Log"]
  datePublished: "2026-07-12"
  publisher: "note"
---

This post, published on note in July 2026 by a writer using the name Hack-Log, is a firsthand account of changing one step of an AI-driven development workflow. The author had been running design, implementation and a final self-review entirely inside [[SoftwareApplication/claude-code]], asking it to review its own code "adversarially", and believed the review worked because tests passed and some findings came back. After reading a remark on X that a model reviewing its own output fails to find holes and drifts toward acceptance even when told to be adversarial, the author noticed that the findings had almost always been about formatting and naming rather than defects in the logic.

The post's remedy is to keep implementation in Claude Code but send only the review to a different model, [[SoftwareApplication/openai-codex]], and it reports that code which had passed self-review as "no problems" promptly yielded bugs. It is an example of what the wiki describes as [[DefinedTerm/cross-model-review]].

## Key Points

- The post's explanation for why same-model self-review misses defects is that "the grader is yourself": an assumption made while writing the code — for example that an input always exists — is carried into the review by the same model, so it never becomes something to doubt.
- It argues that an "adversarial review" prompt changes only the reviewer's surface posture, not the model's underlying assumptions and habits, so posture-dependent issues such as formatting, naming and comments get flagged while assumption-level oversights pass.
- The procedure it describes has three steps: prepare the diff to be reviewed with `git diff` (against the working tree before committing, or a range such as `main...HEAD` after); give it to the other model with a prompt that excludes naming and formatting and asks only for breakable implicit assumptions, edge-case behaviour (empty, null, boundary values, concurrent execution) and places where errors are swallowed; then return the findings to Claude Code to fix.
- The author suggests having Claude Code also check whether each returned finding is actually correct before fixing it, as a filter for mistaken findings.
- The defects the author reports surfacing in their own case were a config-file read that threw an exception and stopped on a first run when the file did not yet exist, an asynchronous operation reported as successful overall even when one part failed, and a place where an error was caught and swallowed without being logged.
- The post presents this as requiring no special tooling — passing `git diff` to a different model and asking it to doubt the assumptions — and suggests trying it on one recent change first. This rests on the author's own experience in their own projects.

## Context

The post is a short personal experiment report; the author describes the blog as a record of AI-and-development experiments done alongside a day job. It does not measure how often the second model's findings were correct or compare models systematically.
