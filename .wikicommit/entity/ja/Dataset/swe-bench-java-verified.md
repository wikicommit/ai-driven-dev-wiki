---
title: "SWE-bench-java-verified"
type: "schema:Dataset"
lang: ja
tags: [ベンチマーク, 評価, コーディングエージェント, ソフトウェアエンジニアリング]
translated_from: ".wikicommit/entity/en/Dataset/swe-bench-java-verified.md"
source_commit: "0905902793f108bf59d40f17ccaecab6d323e38b"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "GitHub のイシュー解決ベンチマークである SWE-bench の Java 版。6 つのオープンソース Java リポジトリから集めた、手作業で検証済みの 91 件のイシューインスタンスで構成され、Docker ベースの評価環境とリーダーボードとともに公開されている。"
---

SWE-bench-java-verified は、Java プロジェクトにおける実際の GitHub イシューを解決するためのベンチマークであり、
多言語のイシュー解決評価に向けた第一歩として、[[Dataset/swe-bench]] の構築ワークフローに従って作られた。
[[ScholarlyArticle/swe-bench-java-a-github-issue-resolving-benchmark-for-java]] で導入され、その著者らは
Docker ベースの評価環境と、今後も保守・更新していくとしたリーダーボードとともに、これを一般公開した。

## 内容

各インスタンスは、GitHub のイシューと、そのイシューが提起された時点のリポジトリの状態からなる。モデルはパッチを
生成しなければならず、与えられたテストケースがすべて通過した場合にのみ、そのイシューは解決済みとみなされる。
構築の過程では、条件を満たす各プルリクエストの詳細（パッチ、ベースコミット、テストパッチ、イシューの記述、
環境セットアップ用のコミット、fail-to-pass テスト）がクロールされた。ベンチマークは 6 つのリポジトリにまたがる
91 件のイシューを含み、FasterXML/jackson-databind に集中している（49 件）一方、最も少ないのは apache/dubbo（4 件）で、
データのシリアライズ、Web サービス、データフォーマット、コンテナツールにわたる。リポジトリはビルドツールとして
Maven または Gradle を使用し、コード行数は約 57,000 行から 457,000 行、イシューの記述は平均約 2,500 文字である。

## 来歴

リポジトリは GitHub 上の人気のある Java リポジトリと [[Dataset/defects4j]] のリポジトリから選ばれ、70 の候補から
19 に絞り込まれた。クロールされた 1,979 件のイシューインスタンスのうち、著者らはまず、決定された実行環境
（ビルドツール、JDK のバージョン、コンパイルコマンド）のもとでリポジトリがコンパイルできたものを残し、次に
fail-to-pass テストが少なくとも 1 つあり、pass-to-fail テストが 1 つもないものを残して、137 件となった。
その後、Java の経験を持つ 10 人の開発者が SWE-bench Verified のアノテーションガイドラインに従ってこれらを精査し、
イシューの明確さ、テストカバレッジ、重大な欠陥を評価した。3 つの基準すべてを満たしたインスタンスのみが残され、
最終的に 91 件となった。

## 用途

これを導入した論文は、GPT-4o、GPT-4o-mini、DeepSeek-V2、DeepSeek-Coder-V2、Doubao-pro を用いた
[[SoftwareApplication/swe-agent]] をこのベンチマークで評価し、解決率が 1.10% から 9.89% の間であったと報告している。
また、同論文の SWE-agent の設定では、すべてのイシューについて実行環境が構成されたわけではなかったと注記している。
