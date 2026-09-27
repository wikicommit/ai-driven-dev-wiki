---
title: "SWE-Bench+"
type: "schema:Dataset"
lang: ja
tags: [ベンチマーク, 評価, コーディングエージェント]
translated_from: ".wikicommit/entity/en/Dataset/swe-bench-plus.md"
source_commit: "90f235c19401779128f2c36166ba9e641fa1393d"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "SWE-bench を改良した派生版。評価対象の LLM の学習カットオフ日以降に作成された 548 件の GitHub イシュー解決タスクからなり、どのイシュー報告やコメントにも解答が含まれないよう選別されている。"
  url: "https://zenodo.org/records/13879453"
  temporalCoverage: "2023-11-01/2024-08-22"
---

SWE-Bench+ は、実世界の GitHub イシュー解決タスクからなるデータセットであり、
[[ScholarlyArticle/swe-bench-plus-enhanced-coding-benchmark-for-llms]] の著者らが [[Dataset/swe-bench]] より
厳密な代替として構築した。著者らが元のベンチマークに見出した 2 つの問題、すなわち評価対象のモデルが学習中に
目にした可能性のあるイシューと、報告やコメントにすでに解答が含まれているイシューを取り除くよう設計されている。

## 内容

このデータセットは、Django を除く SWE-bench と同じプロジェクトから集めた 548 件のタスクインスタンスを含む。
各インスタンスは SWE-bench の形式に従い、イシュー、対応するバージョンのコードベース、そして生成されたパッチの
検証にそのテストが用いられるプルリクエストからなる。論文では、プロジェクトごとのインスタンスの分布が図で示されている。

## 来歴

著者らは SWE-bench のオープンソースのスクリプトを使い、そのデータ収集手法に従った。同じ 12 のプロジェクトを
対象とし、イシューが GitHub の外で管理されている Django は除外したうえで、2023-11-01 から 2024-08-22 までに
作成されたイシューを収集した。この期間は、使用したモデル（GPT-3.5、GPT-4、GPT-4o）のうち最も新しい学習カットオフの
1 か月後から始まる。次に、問題を解決しテストを追加するイシューを残す SWE-bench の属性フィルタと、インストールに
成功しプルリクエストがすべてのテストを通過するイシューを残す実行フィルタを適用し、最後にすべてのインスタンスを
手作業で確認して、イシュー報告に解答の詳細が明示されているものを取り除いた。論文によれば、このデータセットは
SWE-bench プロジェクトのリポジトリへの統合が進められている間、Zenodo で公開されている。

## 利用

導入論文では、GPT-4 と GPT-3.5 を用いた SWE-RAG、GPT-4 を用いた SWE-Agent、GPT-4o を用いた
[[SoftwareApplication/autocoderover]] を SWE-Bench+ で実行し、解決済みとされたパッチを手作業で検証した。
論文は、このデータセットでは [[DefinedTerm/solution-leakage]]（解答リーク）はもはや見られないものの、弱いテストの
問題は残っており、テストを通過したパッチの大半が実際にはイシューを解決していなかったこと、そして各システムの
検証後の解決率が、報告されている SWE-bench の数値を大きく下回ることを報告している。
