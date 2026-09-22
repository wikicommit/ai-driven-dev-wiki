---
title: "Critical Dialogue Review"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-code-review, agents]
sources:
  - type: url
    url: 'https://techblog.zozo.com/entry/ai-development-two-commands'
    hash: sha256:58353a3fded13879de422c6b7cc6aff4012808394657a717d42726f5f81140df
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A review practice, described by ZOZO's core systems division, in which one coding agent produces a design or implementation and a second agent running on a different model criticizes it, the first adjudicates each finding as accepted, rejected or deferred with a recorded reason, and the second then criticizes the rejections and any residual risk. Its stated purpose is independence of perspective, which same-model self-review is argued not to provide."
---

Critical dialogue review is the name [[BlogPosting/ai-driven-development-two-commands]] gives to a review loop run between two coding agents on different models, rather than between a model and itself. In the arrangement described there, [[SoftwareApplication/claude-code]] orchestrates: it generates the design document, implements, judges what to accept and carries out the fixes, while [[SoftwareApplication/openai-codex]] independently investigates the repository's code and criticizes the design and implementation. The stated aim is that an answer produced by one AI is doubted by another from an independent viewpoint.

## Usage

The minimum unit is three rounds. Codex investigates the repository on its own and critically reviews the design or implementation; Claude Code scrutinizes each finding and decides whether to accept it, reject it or hold it, recording the reason either way; Codex then re-criticizes the rejections and any remaining risk. The number of rounds is not fixed — the account states that difficult changes need additional cycles while light ones converge sooner.

What is handed to the reviewing agent is more than a diff. The description is explicit that the practice is not simply passing `git diff` with an instruction to review: the target task's background, purpose, acceptance criteria, implementation detail and design constraints are pulled from the progress table and sent alongside the change. Two axes are reviewed against that material — code quality (bugs, regressions, design defects, security, insufficient tests) and specification conformance (whether the implementation meets the acceptance criteria, whether it is consistent with the stated purpose, whether it follows the implementation policy, and whether it over-implements). In the design phase the same loop is applied at three separate points rather than once at the end: the design document, the task decomposition and the implementation approach, on the stated reasoning that a discrepancy caught at design or decomposition time costs less to fix than one caught after implementation, and that an AI-generated task breakdown can look plausible while diverging from what the existing code actually does.

Prompts and diffs sent to the second agent are checked for secrets — API keys, passwords, tokens — before they leave, which the account presents as an operating rule that has to be built into the command rather than left to the person running it.

## When It Applies

The practice is argued for where quality matters enough to justify the cost, and explicitly not everywhere: the account reports that the Codex pairing takes more time and money than running Claude Code alone, and concludes it is effective for important features and high-risk changes rather than something to use on every task. Claude Code alone is kept as the normal mode and the paired loop offered as a quality-focused one.

It assumes two agents on genuinely different models, and that the reviewing one can investigate the repository for itself rather than seeing only what the first agent shows it. The case made against the cheaper alternative is that a single model is exposed to its own blind spots and to the provider's performance tuning, and that having the same model review its own output — while easy to implement — gives weak independence of perspective.

Its stated failure mode is non-convergence, and the described design treats that as a boundary rather than a defect. Automatic execution runs at most three cycles per review point, and if the same finding remains unresolved across two consecutive cycles the loop switches to interactive. Neither agent is the final judge: where the automatic mode does not converge, the decision returns to a person, which the account describes as part of the quality guarantee rather than a breakdown of it.

How well established it is: this is one division's account of its own deployment, presented as a design rationale rather than as a measured result — the post reports no comparison of defect rates between the paired loop and single-model review, and lists effect measurement among its outstanding work.

## Related Terms

- [[DefinedTerm/closed-loop-ai-review]] — AI on both sides of a pull request, defined observationally from what review events record rather than as a prescribed loop
- [[DefinedTerm/n-version-programming]] — the same appeal to independence between models, applied to generating candidate solutions rather than to criticizing one
- [[DefinedTerm/llm-as-a-judge]] — a model evaluating output, without the adjudication and re-criticism rounds that distinguish this practice
- [[DefinedTerm/agentic-code-review]] — the broader category of code review in which an agent acts as reviewer
- [[DefinedTerm/human-in-the-loop]] — the escalation this practice falls back to when its cycle cap is reached
