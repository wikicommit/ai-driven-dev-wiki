---
title: "LiveCodeBench"
type: "schema:Dataset"
lang: ja
tags: [ベンチマーク, コード生成, 評価, データ汚染]
translated_from: ".wikicommit/entity/en/Dataset/livecodebench.md"
source_commit: "5bacbd79c76dd8cc2c996065acd6063b17df868b"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "コードに関する LLM を評価するための継続的に更新されるベンチマーク。LeetCode、AtCoder、CodeForces のコンテストから時間をかけて収集され、それぞれの公開日がタグ付けされた問題から構築されており、コード生成、自己修復、コード実行、テスト出力予測のシナリオを備える。"
  url: "https://livecodebench.github.io/"
  temporalCoverage: "2023-05/2024-05"
---

LiveCodeBench は、コード関連タスクにおいて大規模言語モデルを評価するためのベンチマークであり、UC Berkeley、MIT、Cornell の研究者らによって [[ScholarlyArticle/livecodebench-holistic-and-contamination-free-evaluation-of-large-language-models-for-code]] で導入された。プログラミングコンテストから新しい問題を継続的に収集し、それぞれに公開日を付与することで、モデルをその学習カットオフ以降に公開された問題だけで評価できるようにしている。著者らはこれを、HumanEval や MBPP のようなベンチマークに代わる、ライブで包括的かつ汚染のない代替として位置づけている。

## 内容

各問題は、自然言語による問題文とテストケース、利用可能な場合には正解の解答、そして公開日として用いられるコンテスト日付を組み合わせたものである。論文執筆時点では、2023 年 5 月から 2024 年 5 月までに公開された 511 問を含んでいた — 内訳は AtCoder から 267 問、LeetCode から 235 問、CodeForces から 9 問 — で、難易度別には easy 182 問、medium 206 問、hard 123 問に分かれ、1 問あたり平均約 17 件のテストがある。問題は 4 つのシナリオに整理されている。コード生成と自己修復（511 の問題インスタンス）、コード実行（85 の LeetCode 問題から抽出した 479 サンプルで、短く実行ステップ数が限られたプログラムに絞り込まれている）、テスト出力予測（181 の LeetCode 問題から得た 442 インスタンス）である。結果は Pass@1 で測定される。

## 来歴

問題は、LeetCode の週次・隔週コンテスト、AtCoder Beginner Contest、CodeForces の Division 3 および 4 のコンテストから、一般に閲覧可能なページのみを対象にスクレイピングされており、画像を含む問題や複数の正解を許す問題は除外されている。難易度ラベルは各プラットフォーム自身のレーティングに基づき、閾値を超えるレーティングの問題は難しすぎるとして除外されている。テストは、利用可能な場合はプラットフォームから取得され、そうでない場合は GPT-4-Turbo が問題の仕様から作成した入力ジェネレーターによって生成され、正しいプログラムに対して検証される。著者らはこれを、新しい問題、シナリオ、モデルが追加されていく拡張可能なフレームワークと説明しており、収集した問題は学術目的にのみ使用し、それらで学習は行わないと述べている。

## 用途

導入論文は LiveCodeBench 上で 52 のモデルを評価し、その公開日を用いて [[DefinedTerm/data-contamination]] の可能性を検出している — たとえば、2023 年 8 月以降に公開された LeetCode 問題で DeepSeek モデルの性能が急落したことなど — また、各モデルのカットオフ以降に公開された問題だけでモデルを比較している。さらに、HumanEval+ で高いスコアを示すファインチューニング済みのオープンアクセスモデルの一部が LiveCodeBench でははるかに低い性能を示すことも報告しており、著者らはこれを HumanEval への過学習と解釈している。
