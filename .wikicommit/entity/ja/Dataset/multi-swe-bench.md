---
title: "Multi-SWE-bench"
type: "schema:Dataset"
lang: ja
tags: [評価, コーディングエージェント, ソフトウェアエンジニアリング]
translated_from: ".wikicommit/entity/en/Dataset/multi-swe-bench.md"
source_commit: "3bb09ff875f75497dbb9ad4d6786745fc33ecce5"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Java、TypeScript、JavaScript、Go、Rust、C、C++ を対象とする、アノテーション済みの 1,632 インスタンスからなる多言語のイシュー解決ベンチマーク。Python 以外のエコシステムにおいて、与えられたイシューに対処するパッチを生成するようにコードベースを修正する能力を、大規模言語モデルについて評価するために構築された。"
---

Multi-SWE-bench は、イシュー解決 — 与えられたイシューに対処するパッチを生成するようにコードベースを
修正するタスク — のためのベンチマークであり、Python 以外のプログラミング言語をカバーするために構築された。
[[ScholarlyArticle/multi-swe-bench-a-multilingual-benchmark-for-issue-resolving]] で提案されたもので、
同論文はその動機として、既存のベンチマーク（同論文はその一例として [[Dataset/swe-bench]] を挙げている）が
ほぼ Python のみに焦点を当てており、そのため多様なソフトウェアエコシステムにわたって大規模言語モデルを
評価するには不十分であることを挙げている。

## 内容

このベンチマークは Java、TypeScript、JavaScript、Go、Rust、C、C++ の 7 言語にまたがる。インスタンスは
合計 1,632 件で、提案論文はこれらを高品質なものと説明している。1 つのインスタンスは、このベンチマークが
中心に据えるイシュー解決タスクを提示する。すなわち、修正対象となるコードベースと、結果として得られる
パッチが対処すべきイシューである。

## 来歴

1,632 件のインスタンスは一括して収集されたのではなく、選別されたものである。提案論文によれば、これらは
68 人の専門アノテーターによって 2,456 件の候補から慎重にアノテーションされたものであり、同論文はこの
アノテーション作業を、ベンチマークが正確で信頼性の高い評価を提供できる理由として挙げている。

著者らはまた、その背後にあるデータ生成パイプライン全体を詳細なチュートリアルとともにオープンソース化して
おり、オープンソースコミュニティが継続的に貢献し、データセットを拡張していくことを促すのがその狙いだと
している。

## 利用

提案論文は、3 つの代表的な手法 — [[DefinedTerm/agentless]]、[[SoftwareApplication/swe-agent]]、
[[SoftwareApplication/openhands]] — を用いて一連の最先端モデルを Multi-SWE-bench 上で評価し、主要な
実証的知見を伴う包括的な分析を報告している。
