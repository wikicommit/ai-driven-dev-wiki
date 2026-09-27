---
title: "InterCode：実行フィードバックを用いた対話的コーディングの標準化とベンチマーク"
type: "schema:ScholarlyArticle"
lang: ja
tags: [ベンチマーク, コード生成, 実行フィードバック]
review_status: pending
translated_from: ".wikicommit/entity/en/ScholarlyArticle/intercode-standardizing-and-benchmarking-interactive-coding-with-execution-feedback.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "対話的コーディングを、コードを行動、実行フィードバックを観測とする標準的な強化学習環境として扱うフレームワーク InterCode を提案し、それを用いて LLM を評価するための Bash、SQL、Python のベンチマークを構築した 2023 年の arXiv 論文。"
  author: ["John Yang", "Akshara Prabhakar", "Karthik Narasimhan", "Shunyu Yao"]
  datePublished: "2023-06-26"
  keywords: ["InterCode", "対話的コーディング", "実行フィードバック", "強化学習環境", "ベンチマーク"]
---

本論文は、人間はコードを対話的に書き、誤りの修正、曖昧さの解消、タスクの分解のために絶えず実行フィードバックに頼っているのに対し、LLM 向けのコーディングベンチマークの多くはコーディングを指示からコードへの静的な変換として扱っている、という観察から出発する。著者らは、この静的な設定では誤りが伝播するおそれがあり、生成されたコードが最終的に実行される環境から切り離されてしまうと論じている。

このギャップを埋めるため、著者らは InterCode を提案する。これは、対話的コーディングを、コードを行動、実行フィードバックを観測とする標準的な強化学習環境として定式化する軽量なフレームワークである。言語やプラットフォームに依存せず、安全で再現可能な実行のために自己完結した Docker 環境で動作し、従来の sequence-to-sequence 型のコーディング手法と互換性を保ちながら、対話的なコード生成のための新しい手法もサポートする。著者らはこれを用いて 3 つの対話的な環境を構築し、そこで最先端の LLM をいくつか評価している。

## 主なポイント

- InterCode は、対話的コーディングを、コードを行動、実行フィードバックを観測とする強化学習環境としてモデル化している。
- 実行は自己完結した Docker 環境で行われ、著者らはこれにより安全で再現可能な実行が得られるとしている。
- 静的なデータセットである NL2Bash、Spider、MBPP のデータを用いて、Bash、SQL、Python を行動空間とする 3 つの対話的なコード環境を構築している。
- [[DefinedTerm/react-prompting]] や Plan & Solve を含むさまざまなプロンプティング戦略で、複数の LLM を評価している。
- 著者らは、結果が対話的なコード生成の利点を示しており、InterCode がコードの理解と生成のための挑戦的なベンチマークとして機能しうると報告している。
- このフレームワークは容易に拡張可能だとされており、その例として Capture the Flag のタスクが挙げられている。論文はこれを、本質的に複数ステップからなり複数のプログラミング言語を伴うものと特徴づけている。

## 補足

本論文は 2023 年 6 月 26 日に arXiv に初めて投稿され、最終改訂は 2023 年 10 月 30 日（バージョン 3）である。著者らはコードとデータをプロジェクトサイト <https://intercode-benchmark.github.io> で公開している。
