---
title: "Cross-model review"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, agentic-code-review, coding-agents]
sources:
  - type: url
    url: 'https://note.com/hacklog_stealth/n/n395c7ca5da82'
    hash: sha256:3e5e8c433b66bc4010afcf256d50e5070473d9728c98a9c9f8174b40a3bb1162
  - type: url
    url: 'https://github.com/alecnielsen/adversarial-review'
    hash: sha256:b6388c19b88afabd80a5fbec468b2934e258bedaf755ba94f82d774704eb71a7
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5"
generated_with: "0.9.0"

properties:
  description: "The practice of having AI-generated code reviewed by a different model from the one that wrote it, rather than asking the implementing model to review its own work, so that the reviewer does not share the implementer's unstated assumptions."
---

Cross-model review is the practice of assigning the review of AI-written code to a different model from the one that implemented it, instead of having the implementing model review its own output. The reasoning given for it in [[BlogPosting/claude-code-self-review-vs-separate-reviewer-model]] is that same-model self-review inherits the implementer's assumptions: whatever the model took for granted while writing the code — that an input exists, that a file is present — it takes for granted again while reading it, so those premises are never questioned. Prompting the same model to review "adversarially" is argued to change only its posture, not those assumptions, whereas a different model does not share them and so asks the questions the implementer never did.

## Usage

Two arrangements illustrate the range, from a one-way hand-off to a symmetric debate.

**One model implements, another reviews.** In the arrangement [[BlogPosting/claude-code-self-review-vs-separate-reviewer-model]] describes, implementation stays with [[SoftwareApplication/claude-code]] and only the review is handed to [[SoftwareApplication/openai-codex]]. The change under review is exported as a `git diff`, and the reviewing model is given a narrowed brief: ignore naming and formatting, and look only for implicit assumptions that can break, behaviour on edge cases such as empty, null, boundary or concurrent input, and places where errors are swallowed. Its findings are then returned to the implementing agent to fix, with the suggestion that the implementer first check each finding is actually correct, filtering out mistaken ones.

**Two models review and debate.** [[SoftwareApplication/adversarial-review]] has Claude and Codex both review the same code independently, then review each other's findings and respond to each other's critiques, before Claude synthesizes the debate, decides which issues are valid and implements the fixes it rates high or medium confidence; the loop repeats until both report no issues. Its README gives the rationale as different models catching different problems, cross-validation filtering out incorrect findings, and agreement between both models marking a high-confidence fix.

## When It Applies

It applies where one model is already writing or reviewing the code alone and a second model can be brought in. It assumes access to a second model that can read the change — in the first account above, nothing more than a diff and a prompt — and a way to carry findings back to whoever fixes the code. The failure it targets is assumption-level defects rather than style: the defects the blog post reports surfacing were a crash on first run when a config file did not yet exist, partially failed asynchronous work reported as success, and an error caught and discarded without logging. The debate form trades cost for that cross-checking: Adversarial Review's README estimates up to about 21 API calls for a review that runs to its default three iterations, and adds a circuit breaker for loops that stop making progress or never reach agreement. The practice rests on one author's report from their own projects and on a tool its author describes as an experimental prototype; neither gives a measurement of how often the second model's findings were right, and the blog post itself recommends verifying findings before acting on them.

## Related Terms

- [[DefinedTerm/agentic-code-review]]
- [[DefinedTerm/adversarial-verification]]
- [[DefinedTerm/critical-dialogue-review]]
- [[DefinedTerm/llm-as-a-judge]]
