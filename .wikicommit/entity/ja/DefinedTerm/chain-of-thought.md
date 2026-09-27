---
title: "Chain-of-Thought プロンプティング"
type: "schema:DefinedTerm"
lang: ja
aliases: ["Chain of Thought"]
tags: [プロンプトエンジニアリング, LLM, 推論]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/chain-of-thought.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Wei らが提案したプロンプティング手法。中間的な推論ステップを示す少数のデモンストレーションを例示として与えることで、モデルが回答の前に自ら一連の中間ステップを生成するようにする。"
---

Chain-of-Thought プロンプティングは、Wei らが [[ScholarlyArticle/chain-of-thought-prompting-elicits-reasoning-in-large-language-models]] で提案した手法であり、少数の Chain-of-Thought のデモンストレーションをプロンプト内に例示として与える。Chain-of-Thought（思考の連鎖）とは一連の中間的な推論ステップのことであり、著者らは、それを生成させることで大規模言語モデルが複雑な推論を行う能力が大幅に向上すると報告している。著者らはこれを単純な手法と説明しており、その中身は例示そのもの、すなわちプロンプト内に置かれた一握りの解答例のデモンストレーションである。

## 用法

論文は、この手法を算術推論、常識推論、記号推論のタスクに適用し、3 つの大規模言語モデルで評価して、3 つのタスク群すべてで改善が得られたと報告している。その目玉となる実証は、プロンプトとしては小さく、効果としては大きい。8 個の Chain-of-Thought の例示を与えられた 540B パラメータのモデルが、数学の文章題のベンチマークである GSM8K で最先端の精度に達し、検証器付きでファインチューニングされた GPT-3 を上回った。つまり、そのベンチマークにおいて、プロンプティングのみの手法が訓練されたベースラインを凌いだということである。

## 適用される場面

著者らがこの手法に付している条件はモデルの規模である。この手法が引き出す推論能力は*十分に大きな*言語モデルにおいて自然に現れると述べており、形式だけで十分だとは示していない。また、プロンプトに例示を置ける few-shot プロンプティングの設定を前提とし、タスクが実際に必要とする中間ステップを示すように例示を書けることを前提としている。その裏付けとなる証拠は論文自身のものであり、算術推論、常識推論、記号推論のタスクにわたる 3 つの大規模言語モデルでの実験である。これは 2022 年 1 月に初めて投稿され、2023 年 1 月に最終改訂されたプレプリントで報告されている。

## 関連用語

[[DefinedTerm/react-prompting]], [[DefinedTerm/prompt-engineering]], [[DefinedTerm/plan-act-observe-loop]]
