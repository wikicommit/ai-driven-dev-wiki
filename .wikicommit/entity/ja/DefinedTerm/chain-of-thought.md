---
title: "Chain-of-Thought プロンプティング"
type: "schema:DefinedTerm"
lang: ja
aliases: ["Chain of Thought", "思考の連鎖"]
tags: [プロンプトエンジニアリング, LLM, 推論]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/chain-of-thought.md"
source_commit: "ef2531ca21f1030c853bca7e560613f050793160"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Wei らによって提案されたプロンプティング手法。中間的な推論ステップを示す少数のデモンストレーションを事例としてプロンプトに与えることで、モデル自身が答えを出す前に一連の中間ステップを生成するようにするもの。"
---

Chain-of-thought プロンプティングとは、Wei らが [[ScholarlyArticle/chain-of-thought-prompting-elicits-reasoning-in-large-language-models]] において提案した手法であり、chain-of-thought のデモンストレーションをいくつか、プロンプト中の事例として与えるものである。chain of thought（思考の連鎖）とは一連の中間的な推論ステップのことであり、それを生成させることこそが、大規模言語モデルの複雑な推論を行う能力を大きく向上させると著者らは報告している。著者らはこれを単純な手法だと説明しており、その実体は事例そのもの — プロンプトに置かれた、ひと握りの解き終えたデモンストレーション — である。

## 使われ方

論文は、この手法を算術推論・常識推論・記号推論のタスクにわたって適用し、3 つの大規模言語モデルで評価して、いずれのタスク群でも改善が得られたと報告している。その目玉となる実証は、プロンプトの分量としては小さく、効果としては大きい。5400 億パラメータのモデルに 8 つの chain-of-thought 事例を与えたところ、算数の文章題のベンチマークである GSM8K において当時の最高精度に達し、検証器を伴うファインチューニング済みの GPT-3 を上回った — つまり、プロンプティングのみの手法が、そのベンチマークにおいて訓練されたベースラインを凌駕したのである。

## 適用される場面

著者らがこの手法に付している条件はモデルの規模である。この手法が引き出す推論能力は*十分に大きな*言語モデルにおいて自然に立ち現れると述べており、したがって形式だけで十分だとは提示されていない。また、事例をプロンプトに置ける few-shot プロンプティングの設定を前提としており、その事例が、タスクが実際に要求する中間ステップを示すように書けることを前提としている。その裏づけとなる証拠は論文自身のものである。すなわち、算術推論・常識推論・記号推論のタスクにおける 3 つの大規模言語モデルでの実験であり、2022 年 1 月に最初に投稿され、2023 年 1 月に最終改訂されたプレプリントで報告されている。

## 関連用語

[[DefinedTerm/react-prompting]], [[DefinedTerm/prompt-engineering]],
[[DefinedTerm/plan-act-observe-loop]]
