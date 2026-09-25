---
title: "Как мы учили Yandex Code Assistant помогать разработчикам с написанием кода и делать их счастливыми"
type: "schema:BlogPosting"
lang: en
tags: [code-completion, developer-experience, evaluation-metrics]
sources:
  - type: url
    url: 'https://habr.com/ru/companies/yandex/articles/841436/'
    hash: sha256:ed090e4e81e25e3fc5fbdddabb08371c8ae7509c5d4943bdcadbc1d5a5459eff
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Yandex engineering post on building the inline code suggestions of Yandex Code Assistant, and in particular on how the team chose and replaced the metrics it used to judge suggestion quality, ending with a composite 'developer happiness' metric."
  author: ["Viktor Ploshikhin"]
  datePublished: "2024-09-12"
  publisher: "[[Organization/yandex]]"
---

This post, published on Habr's Yandex company blog, is written in the first person plural by the head of an ML laboratory in Yandex Infrastructure, who introduces a developer-analyst colleague from the same lab alongside him, and describes how the team built [[SoftwareApplication/yandex-code-assistant]]. The assistant was launched that autumn with free test access on the Yandex Cloud platform, and the authors frame their goal as not only teaching a neural network to write code but making developers satisfied with it.

Most of the post is about measurement. It walks through a sequence of metrics the team relied on — retention as the business metric, an offline unit-test-based metric, an online acceptance rate — and explains why each was insufficient on its own, ending with a composite metric the team calls developer happiness (see [[DefinedTerm/developer-happiness-metric]]).

## Key Points

- After customer interviews and their own experience, the team chose to concentrate on inline suggestions rather than a chat interface, judging inline suggestions to be the part developers actually wanted.
- Retention after the fourth week is used as the business metric: installation was voluntary inside Yandex, so continued use is read as users "voting with their feet". Because it takes a month to measure, the team looked for faster proxy metrics.
- Suggestions are treated as code rather than text: the model predicts complete statements identified through an abstract syntax tree, a truncated statement counts as a bad suggestion, and suggestions must be returned within 500 ms.
- For offline evaluation the team built a metric it calls UnitTest: mask statements in code covered by a unit test, ask the model to predict them, run the test, and count the share that pass. The authors argue this beats edit distance because the same logic can be written in different ways, and it requires no human assessors.
- The team fine-tuned existing models rather than pretraining its own, on its own repository, cutting training targets as statements via tree-sitter and including the case of predicting an empty statement — the post's point being that sometimes saying nothing is better. Fill-in-the-middle ability turned out to matter because people do not write code top to bottom.
- All business logic lives in a CPU backend that decides whether to request a suggestion, enriches context and ranks results, with LLM inference on a separate GPU backend; plugins are kept as thin proxies because fixes to plugins reach users far more slowly. The post reports staying within 420 ms at the 99th percentile.
- Online A/B tests split traffic by request rather than by user, because early audiences were too small for per-user samples to reach significance.
- Acceptance rate rose while the audience began to leave, which the authors take as evidence that acceptance rate can be gamed by showing many short suggestions; this led to the happiness metric, after which retention rose sharply even though acceptance rate initially fell.
- The authors report that 15% of the code developers write in a day is written with the assistant and that 60% of the thousands of Yandex developers who tested it became regular users — figures from the vendor's own measurement.

## Context

The post is a vendor's account of its own product, so the comparisons it reports against competing assistants — including one unnamed as "competitor A" — rest on Yandex's own metric and measurement. Its closing lessons are general: define a product metric, keep an intuitive and quickly computed offline metric, prefer online metrics for the final rollout decision, and do not be afraid to change metrics. For a later Yandex product aimed at non-programmers, see [[BlogPosting/programming-for-those-who-dont-write-code-how-vibecraft-works]].
