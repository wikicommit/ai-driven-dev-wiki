---
title: "NL2Repo-Bench"
type: "schema:Dataset"
lang: ja
aliases: ["NL2Repo Bench"]
tags: [コーディングエージェント, ベンチマーク, 長期タスク]
translated_from: ".wikicommit/entity/en/Dataset/nl2repo-bench.md"
source_commit: "48d80cbbb1b1176580f1d3e42bed65bbe89633ce"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "コーディングエージェントの長期的なリポジトリ生成能力を評価するためのベンチマーク。エージェントは、単一の自然言語の要件ドキュメントと空のワークスペースから、完全にインストール可能な Python ライブラリを構築しなければならない。"
---

NL2Repo-Bench は、[[ScholarlyArticle/nl2repo-bench-towards-long-horizon-repository-generation-evaluation-of-coding-agents]] で提案されたベンチマークであり、コーディングエージェントの長期的なリポジトリ生成能力、すなわち局所的なコード片ではなく完全なソフトウェアリポジトリを構築できるだけの長さにわたって、一貫した推論・計画・実行を維持できるかどうかを評価するために設計されている。

## 内容

各タスクでエージェントに与えられるのは、単一の自然言語の要件ドキュメントと空のワークスペースだけである。そこからエージェントは、自律的にアーキテクチャを設計し、依存関係を管理し、複数モジュールにわたるロジックを実装して、完全にインストール可能な Python ライブラリを作り上げなければならない。結果はテストの合格率として報告され、論文はこれによってこのベンチマークが検証可能なテストベッドになっていると説明している。

## 利用

[[ScholarlyArticle/nl2repo-bench-towards-long-horizon-repository-generation-evaluation-of-coding-agents]] は、最先端のオープンソースおよびクローズドソースのモデルをこのベンチマーク上で評価し、最も強力なエージェントでさえ平均テスト合格率は 40% 未満にとどまり、リポジトリ全体を正しく完成させることはまれだと報告している。同論文は、早期の打ち切り、全体的な一貫性の喪失、ファイル間の脆弱な依存関係、数百ステップに及ぶ対話にわたる不十分な計画といった失敗モードを特定している。
