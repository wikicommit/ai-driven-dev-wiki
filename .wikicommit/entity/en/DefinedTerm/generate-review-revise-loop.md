---
title: "Generate-Review-Revise Loop"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, agents, software-process]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.06065'
    hash: sha256:cb4fdaa0aecd873bb17c7946eae064e6fc7d82ab88b72e25a69a45f06154657d
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An iteration in which a coding agent proposes a patch, a reviewer agent decides whether it resolves the issue and diagnoses what is wrong when it does not, and the original generator revises from that diagnosis — with review as the pivot that turns one-shot patch generation into a closed loop."
---

The generate-review-revise loop is the iteration [[ScholarlyArticle/swe-review]] proposes to close what it calls the open-loop character of AI issue resolution. A coding agent generates a candidate pull request; a reviewer agent, working from the repository but without the golden patch or hidden test results, returns a binary approve or request-changes decision together with a diagnosis naming concrete defects and proposing actionable fixes; patches marked request-changes go back to the original generator with that feedback for revision, while approved patches are kept unchanged. Review is the pivot of the loop rather than a commentary step appended to its end.

## Usage

The loop is what distinguishes the arrangement from one-shot generation, where a candidate pull request is proposed and nothing decides whether the issue was actually resolved. It also supplies the definition of the Resolve Rate after Revision metric, which scores a review operationally by the resolve rate reached after exactly one revision pass conditioned on that review's feedback.

Iterating the loop rather than running it once is where the reported gains come from. On SWE-bench Verified the paper reports resolve rate rising from 27.5% to 56.9% for Qwen3-30B-A3B, from 50.9% to 68.8% for Qwen3-Coder-30B-A3B, and from 72.2% to 75.4% for GLM-5 — much larger gains for the weaker generators than the strong one, which is the shape to expect when the loop's job is to catch and repair failures rather than to improve a patch that already works.

The same structure can be collapsed into a single model: the paper reports training one agent on both issue-resolution and review trajectories, producing a unified generate-review-revise agent rather than a pipeline of separate ones.

## When It Applies

The loop assumes several things are already in place, and they are not incidental. It needs an executable verification harness — grounded issues with hidden test-based checking of resolve status — because both the decision and the diagnosis are evaluated against whether the patch really works. It needs a reviewer that can act in the repository rather than read a diff: the paper's own comparison finds agentic review beating single-turn fixed-context review across all three generator splits, by the widest margin on the harder tasks requiring non-local repository reasoning. And it needs a revision path back to a generator that will act on written feedback.

A failure mode the paper singles out is a correct decision attached to a wrong diagnosis: a reviewer may request changes on a non-resolving patch while identifying the wrong defect, which is why diagnosis quality is audited separately from decision accuracy — semantically against the golden patch, and functionally by whether the text actually helps another agent revise. How much the diagnosis matters is visible in that functional check, run on a sample of 100 instances where the teacher had correctly requested changes: resolve rate after revision was 3.0% with no review, 8.0% with the decision alone, 21.0% with the teacher's full review, and 32.0% with an oracle review. A decision without a usable diagnosis recovers only a small part of what the loop can deliver, and even a good real diagnosis falls well short of an oracle one. These are sample figures for a deliberately hard slice, not comparable with the headline resolve rates above.

Where the paper does count decision errors it finds them shaped by generator quality rather than uniform. Across all three splits Claude Opus 4.6 made 272 errors — 167 false approvals against 105 false rejections — but false approvals were 83% of errors on the strongest generator's split and false rejections slightly predominated, at 57%, on the weakest. The authors read this as reviewer capability mattering most at the frontier: as generators improve, the patch that slips through review becomes increasingly subtle.

As for how well established it is: this is one preprint's framing and one set of measurements, on one benchmark, with candidate patches from three specific models. The underlying idea — that review closes a loop which generation alone leaves open — is presented by the authors as the natural reading of what code review has always done, but the loop under this name and these numbers rests on that single study.

## Related Terms

[[DefinedTerm/agentic-code-review]], [[DefinedTerm/closed-loop-ai-review]], [[DefinedTerm/software-issue-resolution]], [[DefinedTerm/verification-loop]], [[DefinedTerm/code-review-agent]]
