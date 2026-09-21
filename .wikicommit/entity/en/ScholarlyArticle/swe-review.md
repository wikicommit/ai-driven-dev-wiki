---
title: "SWE-Review: Closing the Loop on Issue Resolution with Agentic Code Review"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, agents, benchmarks]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.06065'
    hash: sha256:cb4fdaa0aecd873bb17c7946eae064e6fc7d82ab88b72e25a69a45f06154657d
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A preprint arguing that one-shot pull-request generation by coding agents is open-loop, and proposing agentic code review as the mechanism that closes it: a reviewer agent that explores the repository, returns a binary accept/request-changes decision, and writes a structured diagnosis a revision agent can act on."
  author: ["Ruoyu Wang", "Jierun Chen", "Shaowei Wang", "Chaofan Tao", "Sidi Yang", "Yuxin Jiang", "Kim-Hui Yap", "Lifeng Shang", "Xiaohui Li", "Haoli Bai"]
  datePublished: "2026-07-07"
  keywords: ["Agentic Code Review", "Issue Resolution", "Coding Agents", "Test-Time Scaling"]
---

This paper starts from an observation about how coding agents are currently used on real software issues: an agent proposes a pull request and that is the end of the process. The authors call this open-loop — once a candidate PR exists there is no reliable mechanism for deciding whether the issue was actually resolved, nor for diagnosing what should change when it was not. Their proposal is that code review is the natural mechanism for closing that loop, because a reviewer produces exactly the two outputs the loop needs: a binary decision, and an account of what is wrong and how to fix it.

The paper formalizes [[DefinedTerm/agentic-code-review]] as a repository-grounded task. A review instance gives the reviewer a repository checkout at the relevant commit, a natural-language issue, and a candidate PR with its diff, title and body — but not the golden patch and not the hidden test results. The reviewer may browse files, search code, inspect dependencies and run commands before submitting a report containing a decision and, where it requests changes, a diagnosis citing concrete defects and code locations. Three metrics evaluate that report by its role in issue resolution rather than against reference comments: Completion Rate (whether a parseable review is produced at all), Decision Accuracy (the approve/request-changes call against the patch's true resolve status, with unparseable reviews scored 0.5), and Resolve Rate after Revision (the final resolve rate once request-changes patches are returned to the original generator for one revision).

Around that formulation the paper builds two released artifacts — [[Dataset/swe-review-bench]] for evaluation and [[Dataset/swe-review-traj]] for training — and studies agentic review in three roles: as a reviewer of candidate PRs, as supervision for training open reviewers and issue-resolution models, and as a verifier for test-time scaling.

## Key Points

- The paper's central claim is that agentic code review is a practical mechanism for moving AI coding agents from one-shot PR generation toward closed-loop issue resolution, rather than a post-hoc commenting tool.
- Iterating a [[DefinedTerm/generate-review-revise-loop]] on SWE-bench Verified raised resolve rate from 27.5% to 56.9% for Qwen3-30B-A3B, from 50.9% to 68.8% for Qwen3-Coder-30B-A3B, and from 72.2% to 75.4% for GLM-5 — the largest gains accruing to the weakest generator.
- Agentic review outperformed single-turn fixed-context review baselines on both Decision Accuracy and Resolve Rate after Revision across all three PR-generator splits, with the largest margins on tasks the authors classify as harder and as requiring non-local repository reasoning.
- Supervised fine-tuning an 8B model on the paper's review trajectories raised its completion rate from approximately 4% to 71–84% and its decision accuracy from near-random to 67–72%.
- Mixing review trajectories with issue-resolution training data improved direct resolve rate by up to 5.6 points and produced a unified generate-review-revise agent with up to a 10.6-point gain in final resolve rate — the paper's evidence that review supervision transfers beyond the review task itself.
- At test time, reviewers trained on these trajectories outperformed dedicated verifiers on both effectiveness and efficiency, and review-guided iterative revision raised resolve rate from 22.9% to 38.4% over four revision rounds.
- An ablation on how much of the review matters reports resolve rates after revision of 3.0% with no review, 8.0% with the decision alone, 21.0% with the teacher's full review, and 32.0% with an oracle review — the authors' evidence that the diagnosis, not just the accept/reject call, is what carries the gain.

## Notes

The authors state they will release the benchmark, the review trajectories and the reviewer models. The benchmark's candidate PRs and the PRs underlying the training trajectories come from the same three models (GLM-5, Qwen3-Coder-30B-A3B, Qwen3-30B-A3B), so the quality distribution the reviewers are measured against is a property of those particular generators rather than of AI-authored pull requests generally. The trajectories themselves are not those models' work: each is one review of a candidate PR by a single teacher — open-weight GLM-5 with thinking enabled, under the OpenHands-SDK scaffold — chosen over a closed model so that the traces would be complete and transparent.

The paper reports its own checks on diagnosis quality and is explicit about their limits. Two proprietary judges scoring diagnoses on a 1–5 scale for factual accuracy, fix correctness and grounding in repository evidence returned mean scores just above 3.0, which the authors read as "meaningful valid information even though they are not perfect" rather than as high quality; inter-judge agreement was substantial (Cohen's κ = 0.72). A stricter filter requiring both judges to score at least 3 cut the trajectory set from 8,914 to 6,789 but, the authors report, produced no clear benefit over decision-correctness filtering alone.
