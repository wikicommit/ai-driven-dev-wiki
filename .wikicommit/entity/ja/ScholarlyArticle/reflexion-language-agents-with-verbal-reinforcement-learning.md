---
title: "Reflexion：言語による強化学習を行う言語エージェント"
type: "schema:ScholarlyArticle"
lang: ja
tags: [LLM エージェント, 自己省察, コード生成]
review_status: pending
translated_from: ".wikicommit/entity/en/ScholarlyArticle/reflexion-language-agents-with-verbal-reinforcement-learning.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM ベースのエージェントを、重みの更新ではなく言語的フィードバックによって改善するフレームワーク Reflexion を提案した 2023 年の arXiv 論文。エージェントはタスクのフィードバックについて言語で振り返り、その振り返りをエピソード記憶に保存して以降の試行に活用する。"
  author: ["Noah Shinn", "Federico Cassano", "Edward Berman", "Ashwin Gopinath", "Karthik Narasimhan", "Shunyu Yao"]
  datePublished: "2023-03-20"
  keywords: ["Reflexion", "言語エージェント", "言語による強化学習", "エピソード記憶"]
---

この論文は、ゲーム、コンパイラ、API といった外部環境と相互作用する目標駆動型エージェントとして大規模言語モデルを用いる際の限界を扱っている。従来の強化学習は大量の訓練サンプルと高コストなファインチューニングを必要とするため、試行錯誤から素早く学習することが難しい。論文は、モデルの重みを更新するのではなく言語的フィードバックによって言語エージェントを強化するフレームワークである [[DefinedTerm/reflexion]] を提案している。

Reflexion エージェントは、タスクのフィードバック信号について言語で振り返り、得られた振り返りのテキストをエピソード記憶バッファに保持し、それを以降の試行でより良い意思決定を行うために用いる。著者らは、逐次的意思決定、コーディング、言語推論のタスクにわたってこれを評価し、ベースラインのエージェントに対して大幅な改善を報告している。

## 要点

- このフレームワークは、重みの更新やモデルのファインチューニングではなく、言語的フィードバックによってエージェントを強化する。
- エージェントはタスクのフィードバック信号について言語で振り返り、その振り返りのテキストをエピソード記憶バッファに保持して以降の試行の指針とする。
- このフレームワークは、さまざまな種類（スカラー値または自由形式の言語）と出所（外部、または内部でシミュレートしたもの）のフィードバック信号を受け付ける。
- 著者らは、逐次的意思決定、コーディング、言語推論のタスクで、ベースラインのエージェントに対する大幅な改善を報告している。
- HumanEval コーディングベンチマークでは、pass@1 正解率 91% を報告しており、論文がそれ以前の最高水準とする GPT-4 の 80% を上回っている。
- 論文には、異なるフィードバック信号、フィードバックの取り込み方法、エージェントの種類についてのアブレーションと分析の研究が含まれている。

## 補足

この論文は 2023 年 3 月 20 日に arXiv に初投稿され、2023 年 10 月 10 日に最終改訂された（第 4 版。コメントによればいくつかの実験が追加されている）。Artificial Intelligence、Computation and Language、Machine Learning の分野に分類されている。
