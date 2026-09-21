---
title: "コーディングガイドライン運用をAIで自動化し、レビュー知見を資産化する"
type: "schema:BlogPosting"
lang: en
tags: [agents, code-review, github-actions]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62639/'
    hash: sha256:8fe61a90b7d83235354ba7e66eb8068f7329ab03406aa10fc3725f34ee02cadc
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A CyberAgent frontend engineer's account of a GitHub Actions workflow that harvests pull-request review comments, has an AI distill them into coding-guideline candidates, and opens a pull request where humans decide which become team rules — with the stated aim of turning review knowledge into a durable asset."
  author: ["yuuumin"]
  datePublished: "2026-03-12"
  publisher: "[[Organization/cyberagent]]"
---

This post describes a mechanism for keeping coding guidelines continuously updated from the pull-request review comments a team already produces. The author, a web frontend engineer in CyberAgent's AmebaLIFE division, frames the problem as one that gets sharper the more development leans on AI: unless a team's judgment criteria and review perspectives are organized, output quality does not stabilize — and, separately, that both humans and AI then find it harder to work from the same assumptions.

Two specific problems are named. Review knowledge stays buried in pull requests and rarely becomes a team asset — useful in the moment, but closed between the reviewer and the reviewed, and easily lost with time. And a guideline document, once written, tends not to be updated, drifting away from actual review perspectives until nobody reads it. The author restates the problem as being not the absence of guidelines but that tacit knowledge is not being put into words, and that what is written is not kept up.

The response is a GitHub Actions workflow that collects review comments over a period, has an AI analyze them into guideline candidates presented as a pull request, lets humans decide what to adopt, syncs that decision into the document, and merges. The post is explicit that the deciding step is deliberately human, and reports the effects as early observations from a recently introduced mechanism rather than as measured results.

## Key Points

- The workflow runs in two phases: `extract`, which builds a pull request of guideline candidates from review comments, and `sync`, which writes the accepted decisions back into the document.
- `extract` runs on `schedule` and `workflow_dispatch` — scheduled normally, manual during rollout — and defaults to the previous seven days when no range is given. The post's stated reason for bounding the period is to limit how much information the AI is given, so extraction accuracy holds.
- The candidate pull request lists each guideline with a priority, background and citation, plus an "exclude" checkbox — the worked example in the post also shows a category field. Checked items are treated as excluded, and if every item is excluded the pull request is closed automatically.
- `sync` is triggered by `pull_request: edited` but restricted to pull requests carrying a dedicated label, which the post gives as a way of holding down GitHub Actions execution cost.
- `sync` reads only a machine-readable metadata block embedded in the pull request body — not the body as a whole — which the post argues keeps the sync from breaking when headings or explanatory prose change, and avoids introducing a second storage location.
- The whole job — comment collection, AI execution, pull-request creation, decision sync, commit and push — is packaged as a GitHub reusable workflow, so an adopting repository only defines its triggers and a `uses:` line.
- The stated reason for [[DefinedTerm/human-in-the-loop]] is that guidelines become team norms rather than summaries: review comments can depend on repository-specific circumstances, release priorities at the time, exceptions deliberately allowed, or a knowingly taken trade-off, and letting an AI finalize candidates without that context risks leaving wrong guidelines in place. The AI is given the role of proposing candidates and the human the role of deciding what stands as a norm.
- Three effects are reported as early observations: perspectives added to the guidelines began appearing as findings in [[SoftwareApplication/claude-code]]'s Code Review, which the team had adopted, with insufficient Storybook state coverage given as an example; human review became easier to focus on specification validity and business logic once baseline perspectives were being caught automatically; and a perspective, once written down, no longer has to be rediscovered from scratch in later reviews.
- The author's own summary of the aim is three things: putting tacit knowledge into words, turning review knowledge into an asset, and converting tacit knowledge into organizational knowledge.
- No measurement is given for any of the reported effects — the post states the mechanism was only recently introduced.

## Context

The post is explicit that general best practices already exist in abundance, and that what it is after is the part those do not cover: the perspectives and trade-offs each team weighs slightly differently, which general guidance cannot supply and which otherwise have to be re-agreed at every implementation and review.

Its stated open questions are about scale and transfer rather than mechanism: which period granularity best balances accuracy against operational load, how to maintain guidelines across multiple repositories, whether the shape is transferable to other teams and job functions, how to extract judgments and trial-and-error from local AI chat sessions rather than pull-request reviews alone, and what further AI work the assembled guidelines could support.

The closing argument is that coding guidelines are harder to keep growing than to create, which is the author's stated reason for designing the split between what AI is given and what humans decide as an operational practice rather than a one-off document.
