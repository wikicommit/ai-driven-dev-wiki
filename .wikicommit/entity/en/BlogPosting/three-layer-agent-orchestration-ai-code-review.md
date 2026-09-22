---
title: "3層エージェントオーケストレーションで実現する高精度AIコードレビュー"
type: "schema:BlogPosting"
lang: en
tags: [agentic-code-review, multi-agent, agent-orchestration, coding-tools]
sources:
  - type: url
    url: 'https://techblog.openwork.co.jp/entry/ai-code-review-3-layer-architecture'
    hash: sha256:b4d6c939c7b4971dd50b6e2277243cbceb4d415eaf799742f1d75acf18a48570
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An OpenWork engineer's account of a three-layer code review system built from GitHub Copilot CLI custom agents, in which review perspectives are split across dedicated agents and only findings that two or more independent agents raise are kept."
  author: "Yamamoto (k_yamamoto_ow)"
  datePublished: "2026-03-31"
  publisher: "OpenWork"
---

This post describes a code review system the author built to address three complaints about single-agent AI review: that finding quality stays unstable even when skills and instructions are well developed, that trivial findings and hallucinations are frequent, and that the same point is raised repeatedly across rounds. The proposed answer is [[DefinedTerm/three-layer-agent-orchestration]] — splitting review into per-perspective agents, running each perspective several times over, and keeping only what independent runs agree on.

What distinguishes the account from a design sketch is that it reports the system in production with team feedback, and states its own evaluation as not yet done: the author sets out three quantitative criteria with an 80% pass line for each and describes them as future work, explicitly conditioning any handover of review work to agents on meeting them first.

## Key Points

- The system is organized in three layers: a parent agent that decides which technical domains a branch touches and orchestrates the run; a middle layer of context-collection, static-analysis and review-scrutiny agents; and a bottom layer of review agents each confined to one perspective.
- Which agents launch is decided mechanically from changed-file extensions — PHP files other than tests select backend perspectives and PHPStan, TypeScript/JavaScript/Vue/Twig select frontend perspectives with ESLint and type checking, and test files (`*Test.php`, `*.spec.ts`) select a test-design perspective instead. A PR spanning domains launches the agents for each.
- Each perspective is reviewed by four agents in parallel, and the scrutiny agent keeps only findings that two or more of them raise about the same place for the same reason. The author's stated rationale is that a finding raised by one agent alone is likely to be a hallucination, an overreaction or trivial.
- The four agents are deliberately split across two model families — two running Claude Opus 4.6 and two running GPT-5.4 — so that model-specific biases and hallucination patterns cancel rather than reinforce. The author argues that agreement across vendors is stronger evidence of a real problem than agreement within one.
- Review agents operate under four prohibitions, all aimed at keeping each agent on the change in front of it: no praising good points, no proposing implementations, no findings that violate YAGNI, and no findings about existing code outside the change. The author names two of them — the ban on implementation proposals and strict adherence to YAGNI — as effective specifically against noise peculiar to AI review. The separation of reviewing from fixing is argued for explicitly — fixing belongs to whichever coding agent does the fixing.
- Project-specific knowledge reaches the agents by pointing each at the relevant existing skill file, such as an onion-architecture guideline for the architecture perspective. The author states a preference for migrating review perspectives wholesale into skills and launching one review agent per skill, describing the perspective files written for this system as an interim arrangement.
- Findings are posted as inline comments on the pull request, together with the user's original prompt, which the author presents as making review history visible to other engineers, letting a coding agent be pointed at the comments to do the fixing, and making the instructions behind a review auditable.
- A context-collection agent reads the PR's existing review comments and replies and classifies them into already-raised points and points an engineer has declined, passing both forward. The declined category is treated as a standing instruction across the whole review rather than a per-location one, so that a "this is out of scope" reply suppresses the same finding elsewhere in the PR.
- Reported team feedback is favorable but qualitative: reviewers valued readability findings that a plain agent review did not surface, catching dead code missed during compaction, and being able to see which perspectives produced which findings and how the filter resolved them.
- The author frames a three-level split of review difficulty — findings decidable from the changed lines alone, findings needing several places in the codebase, and findings needing knowledge outside the code such as specification fit, UX and domain understanding — and assigns the first two to tools and agents while reserving the third for engineers.

## Context

The post is written from inside a team that had already adopted GitHub Copilot across its developers, and the author is explicit that the design depends on that: because the custom agents launched by another agent do not consume the premium-request unit the plan bills on, adding agents for precision could be decided without weighing cost. That is a statement about the arrangement the team was working under at the time of writing, and it is the stated reason a design launching dozens of agents was affordable at all.

The author addresses vendor-provided review capabilities directly, arguing that an in-house system retains an advantage in that engineers can adjust its procedure and perspectives freely. The post anticipates that such capabilities will improve and become cheaper, and states an intention to migrate once using one costs less than maintaining a system in-house. The author also reports being pleased that the approach taken here — several agents reviewing and their results filtered — appeared to line up with the direction a major vendor had taken, and treats that as corroboration that the design was sound.

See also [[DefinedTerm/agentic-code-review]] and [[BlogPosting/ai-code-review-ideal-and-reality]].
