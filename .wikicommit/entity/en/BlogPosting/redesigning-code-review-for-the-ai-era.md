---
title: "コミット数2倍でもレビュー品質を維持！AI時代のコードレビューフロー再設計"
type: "schema:BlogPosting"
lang: en
tags: [code-review, agents, testing, software-process]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60882/'
    hash: sha256:7997cccac08ed6a2731d85a3012e81cea6de4b141192497c171f97de0740feb1
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A firsthand account of one team's redesign of its code review flow after adopting coding agents roughly doubled its commit count, covering monorepo guidelines, a shift-left testing strategy, standardized agent skills, three parallel AI reviewers, and making AI the final gate after human approval."
  author: "minhquang"
  datePublished: "2025-12-18"
  publisher: "CyberAgent"
---

The post begins from an asymmetry rather than from a tool. After the author's team adopted Cursor, Claude Code and Codex about six months earlier, its commit count roughly doubled — but, as the post puts it, a matching doubling of the hours engineers spend reviewing is hard to arrange. Left alone, that gap comes out as falling code quality, which makes the [[DefinedTerm/review-bottleneck]] the binding constraint on the productivity the agents were supposed to deliver.

What the post argues is that the answer is not to review harder but to redesign the flow around two aims stated up front: raise the quality of pull requests *before* they reach review, so there is less for a human to do, and make the reviewing itself faster. The responsibilities themselves are held fixed — the author states that the division between reviewee (implement appropriately, be able to explain your code, assure its quality) and reviewer (guarantee the merge bar is met, decide approve or reject) is the same in the AI era as before.

The measures described are concrete and mostly structural: unified monorepo guidelines written to hold only what an AI does not already know, a testing strategy it adopted under the name [[DefinedTerm/testing-skyscraper]], under which its backend team's test-to-code line ratio passed 100%, standardized skills and slash commands for routine agent work, three AI review tools running in parallel, and, last of the measures it describes, moving the final gate from a human to an AI.

## Key Points

- The framing claim: review load is where agent-driven productivity gains are lost, because implementation speed scales with agents while human review capacity does not, and AI-generated code is harder for a human to find faults in.
- On guidelines, the post's rule is to write down only what is team-specific: the AI already holds general knowledge, so guidelines should carry team conventions, chosen approaches and business-domain knowledge. Its worked contrast is that "handle errors appropriately" is too generic to be worth writing, whereas a rule mandating `ConditionExpression` and optimistic locking for DynamoDB operations, or requiring `auth.GetUserID()` rather than reading the user ID from context directly, is not.
- The monorepo keeps common guidelines in `docs/guidelines/` and per-area ones under `{backend|frontend|native}/docs/guidelines/`, treated as the single source of truth; because agents differ in how they load guidance, each agent's own configuration references those files rather than restating them.
- The team set aside the usual test pyramid's proportions (unit 70–80%, integration 15–25%, E2E 5–15%) for the position that every layer is good and any may be written heavily where needed, on the argument that in an era of rapid change more integration and E2E coverage is needed, not less — reporting its backend team's test-to-code line ratio rising from 78.6% in June 2025 to 95.2% in September and 112.6% by December.
- It argues the maintenance objection to more tests has largely dissolved: a guideline telling the agent to update the tests when it changes the code means the agent mostly does it. The execution-time objection has not dissolved, and the team's answer is scheduling — GitHub Merge Queue runs only lightweight tests at PR creation and defers heavy E2E runs until after review approval.
- Routine agent work is standardized into four skills — `creating-pull-requests`, `fixing-ci-failures`, `handling-review-comments` and `reviewing-pull-requests` — provided as both skills and slash commands, the post notes, because Cursor had no skills feature when it was written.
- Three AI reviewers run at once (GitHub Copilot, [[SoftwareApplication/greptile]] and [[SoftwareApplication/claude-code-action]]), which the post defends as deliberate: the field is in transition, so for now the team wants several models looking from different angles, and says it may later evaluate and choose which services to keep. On the author's account team feedback rates Greptile and Claude Code Action higher, and the author's own preference is Greptile for its ability to learn from review comments and auto-generate custom rules.
- The custom Claude Code Action review flow is split into four phases with subagents by concern: gathering PR metadata and the applicable guidelines, reviewing per perspective against them, a severity-evaluation subagent that judges whether each AI comment is valid and not fabricated, and a posting phase that inline-comments only the high-severity findings and avoids duplicating what another agent already said.
- The post reports that customizing the flow this way produced noticeably better review quality than simply handing over the guidelines and asking for a review — an assessment from the team's own experience, with no measurement offered.
- On making AI the final gate, the stated motivation is that any process with a human in it unavoidably carries the possibility of oversights and operational mistakes; the account of the result — that reviewer and reviewee can now merge with confidence — is likewise the author's own judgment rather than a measured outcome.

## Context

This is one company's engineering-blog post, written for a 2025 Advent Calendar by a backend engineer at CyberAgent's Hanoi Development Center, and it reads as a report from inside one team rather than as general guidance. It opens by noting that CyberAgent had rolled out company-wide support of $200 per engineer for AI agent costs, and that the author's team adopted Cursor, Claude Code and Codex about six months before writing.

Its evidential character is uneven in a way worth keeping in view: the test-ratio figures and the commit-count doubling are the team's own measurements, while the comparative assessment of the three review tools, the claim that the customized flow reviews better, and the verdict on the AI gatekeeper are stated as team impressions. The author closes by framing all of it as a stage rather than a conclusion, saying the flow will keep being revisited as the technology changes.
