---
title: "Chain-of-Thought プロンプティング"
type: "schema:DefinedTerm"
lang: ja
aliases: ["Chain of Thought"]
tags: [プロンプトエンジニアリング, LLM, 推論]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/chain-of-thought.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Wei らが提案したプロンプティング手法。中間的な推論ステップを示す少数のデモンストレーションを例示（exemplar）として与えることで、モデルが回答の前に自ら一連の中間ステップを生成するようにする。"
---

Chain-of-Thought プロンプティングとは、Wei らが
[[ScholarlyArticle/chain-of-thought-prompting-elicits-reasoning-in-large-language-models]] で提案した手法であり、
少数の chain-of-thought のデモンストレーションをプロンプト内の例示（exemplar）として与えるものである。chain of thought とは
一連の中間的な推論ステップのことであり、著者らは、それを生成することが大規模言語モデルの複雑な推論能力を大幅に向上させると報告している。
著者らはこれを単純な手法だと述べており、その中身は例示そのもの、つまりプロンプトに置かれた少数の解き方を示したデモンストレーションである。

## 用法

論文は、この手法を算術推論、常識推論、記号推論のタスクに適用し、3 つの大規模言語モデルで評価して、3 つのタスク群すべてで改善が見られたと報告している。
その代表的な実証は、プロンプトの観点では小さく、効果の点では大きい。8 つの chain-of-thought の例示を与えられた 540B パラメータのモデルが、
数学の文章題のベンチマークである GSM8K で最先端（state-of-the-art）の精度に達し、検証器（verifier）付きでファインチューニングされた GPT-3 を上回った。
つまり、そのベンチマークにおいて、プロンプティングのみの手法が学習済みのベースラインを上回ったということである。

## 適用される場面

著者らがこの手法に付している条件はモデルの規模である。この手法が引き出す推論能力は *十分に大きな* 言語モデルにおいて自然に創発すると述べており、
形式だけで十分だとはしていない。例示をプロンプトに置くことのできる few-shot プロンプティングの設定を前提としており、
またその例示が、タスクが実際に必要とする中間ステップを示すように書けることを前提としている。その裏づけとなる証拠は論文自身のものであり、
算術推論、常識推論、記号推論のタスクについて 3 つの大規模言語モデルで行った実験が、2022 年 1 月に最初に投稿され 2023 年 1 月に最終改訂されたプレプリントで報告されている。

## 関連用語

[[DefinedTerm/react-prompting]], [[DefinedTerm/prompt-engineering]],
[[DefinedTerm/plan-act-observe-loop]]
