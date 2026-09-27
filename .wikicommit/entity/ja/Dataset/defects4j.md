---
title: "Defects4J"
type: "schema:Dataset"
lang: ja
tags: [プログラム修復, ベンチマーク, Java]
translated_from: ".wikicommit/entity/en/Dataset/defects4j.md"
source_commit: "029a1c18064c79f7a24b408c62abfa180a4f512c"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "自動プログラム修復の手法を評価するために広く用いられている、17 の Java プロジェクトに由来する 835 件の実世界のバグからなるベンチマーク。バージョン 1.2 の 6 プロジェクト由来の 395 件と、バージョン 2 で追加された 11 プロジェクト由来の 440 件に分かれる。"
---

Defects4J は、Java プロジェクトに由来する実世界のバグのデータセットであり、[[DefinedTerm/automated-program-repair]] の手法を評価するベンチマークとして広く用いられている。ここでの記述は、このデータセット全体で評価を行っている [[ScholarlyArticle/repairagent-an-autonomous-llm-based-agent-for-program-repair]] に基づく。

## 内容

データセットは 17 の Java プロジェクトに由来する 835 件の実世界のバグからなる。内訳は、Defects4J v1.2 の 6 プロジェクト由来の 395 件と、Defects4J v2 で追加された 11 プロジェクト由来の 440 件である。各バグには少なくとも 1 つの失敗するテストケースが付属する。プロジェクトには Chart、Cli、Closure、Codec、Collections、Compress、Csv、Gson、JacksonCore、JacksonDatabind、JacksonXml、Jsoup、JxPath、Lang、Math、Mockito、Time が含まれ、最大のものは 174 件のバグを持つ Closure である。RepairAgent の著者らは、正解の修正が平均で 2.9 行を追加して 9.3 行を削除し、平均 381 トークンを変更すると報告している。

## 利用

[[ScholarlyArticle/repairagent-an-autonomous-llm-based-agent-for-program-repair]] は、835 件のバグのうち 164 件を正しく修正し、ChatRepair、ITER、SelfAPR と比較している。比較には、それぞれの手法の著者らが提供したパッチを用いている。汎化性とデータ漏洩の影響の可能性を評価するため（同論文が用いたモデルである GPT-3.5 は、学習時にこれらの Java プロジェクトの一部を見ている可能性がある）、同論文は 2023 年に修正されたバグからなる、より新しい GitBug-Java データセットでも追加の評価を行っている。これとは別に、各バグに少なくとも 1 つの失敗するテストケースがあるという Defects4J の保証は実際の利用では成り立たない場合があることを限界として挙げ、そのようなテストのないバグでの評価を今後の課題としている。
