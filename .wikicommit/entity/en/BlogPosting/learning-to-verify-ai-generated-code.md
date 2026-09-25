---
title: "Learning to Verify AI-Generated Code"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, verification, evaluation]
sources:
  - type: url
    url: 'https://openhands.dev/blog/20260305-learning-to-verify-ai-generated-code'
    hash: sha256:672e965c31f9cb19e39209c68cf05a7789cd6435e662e2fbef87b99f6c790dfe
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An OpenHands blog post arguing that verification, not code generation, is now the bottleneck for coding agents, and introducing a small critic model, trained on real-world production traces, as the first layer of what OpenHands calls a verification stack."
  author: ["Xingyao Wang"]
  datePublished: "2026-03-05"
  publisher: "OpenHands"
---

This post from the [[SoftwareApplication/openhands]] blog starts from the claim that LLMs made
generating code cheap and that the real bottleneck is now verification: checking that a change is
correct, follows the repository's conventions, and is something a team can trust, review and merge.
OpenHands frames its answer as a **verification stack** — a layered set of verifiers meant to help
coding agents fail fast and produce changes humans can confidently merge — and the post introduces the
first layer of that stack: a trajectory-level verifier implemented as a small, fast
[[DefinedTerm/critic-model]].

Its central argument is about where such a critic's training signal comes from. Earlier academic work,
the post says, trained critics on benchmark datasets where verified rewards such as unit tests label each
attempt correct or not; production, human-in-the-loop development usually has no such rewards, and the
post reports that critics trained only on benchmark traces translate poorly to it. OpenHands therefore
trains its critic on real-world user–agent interactions, turning sparse production signals into dense
supervision through rubrics. The post defers a second, patch-level layer of the stack to a follow-up post.

## Key Points

- The post states that the bottleneck for AI coding has moved from generating code to verifying it.
- OpenHands describes its approach as a verification stack of layered verifiers; this post covers only the first layer, a critic that scores an agent's whole trajectory (conversation, tool calls and actions).
- The critic's score is presented as usable to decide whether to continue, stop or refine, to pick among multiple attempts, and to collect lightweight feedback that improves the agent over time; because the model is small, the post says it is fast (often sub-second to about a second) and cheap enough to run during an interactive session.
- By the post's own measurements, a critic trained only on benchmark-style data scored an AUC of about 0.45–0.48 on production outcomes, worse than random, against 0.58 when trained with PR merge as the outcome proxy and 0.69 with code survival as the proxy.
- Its training pipeline splits each interaction into segments (user request, agent actions and tools, finish), annotates every segment with 24 trace-observable "Critic Rubrics" features describing behavioural quality and common failure modes such as misunderstood intent, not following instructions and scope creep, and grounds a subset of segments in sparse outcomes — code survival for about 4% and PR merge for about 6%.
- OpenHands reports running regressions from the rubric features to sparse outcomes and concludes that rubrics are predictive of real outcomes, and that what is predictive can differ between benchmarks and production.
- The critic itself is a small semi-supervised, multi-task model that learns to predict the dense rubric features and success from the sparse outcome proxies.
- On the mixed-outcome subset of SWE-bench Verified (instances where at least one run succeeds and at least one fails), the post reports critic-guided best-of-8 selection at 73.8% against 57.9% for random selection, and early stopping 17.7 points above random with 1.35 attempts on average instead of 8.
- These results are OpenHands' own evaluation of its own critic, and the post refers readers to an accompanying paper for the full ablations.
- The critic is integrated into the OpenHands Software Agent SDK for programmatic use (reranking, early stopping, iterative refinement) and, with early stopping and configurable acceptance thresholds, into the OpenHands CLI.

## Context

The post positions its critic against benchmark-trained critics from earlier academic work rather than
against other production verifiers, and its central claim — that real-world supervision is necessary
because benchmark-trained critics do not transfer — rests on OpenHands' own production data and
evaluation. It is published by the vendor of the agent the critic is built for, and closes by inviting
teams deploying OpenHands to get in touch about wiring critic-based verification into their workflows.
Judging a trajectory rather than only its final output is the same distinction this wiki records as
[[DefinedTerm/trajectory-evaluation]].
