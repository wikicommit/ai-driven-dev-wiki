---
title: "複雑さの罠：エージェントのコンテキスト管理において単純な観測マスキングは LLM による要約と同等に効率的である"
type: "schema:ScholarlyArticle"
lang: ja
tags: [コンテキスト管理, コーディングエージェント, エージェントの効率]
translated_from: ".wikicommit/entity/en/ScholarlyArticle/the-complexity-trap.md"
source_commit: "48d80cbbb1b1176580f1d3e42bed65bbe89633ce"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "LLM ベースのソフトウェアエンジニアリングエージェントにおけるコンテキスト管理戦略を比較した 2025 年の arXiv 論文。古い環境観測を単純にマスクするだけで、素のエージェントに比べてコストが半減し、しかも LLM による要約と同等の解決率が得られることを示し、両者を組み合わせたハイブリッド手法を導入している。"
  author: ["Tobias Lindenbauer", "Igor Slinko", "Ludwig Felder", "Egor Bogomolov", "Yaroslav Zharov"]
  datePublished: "2025-08-29"
  keywords: ["観測マスキング", "LLM による要約", "コンテキスト管理", "ソフトウェアエンジニアリングエージェント"]
---

LLM ベースのエージェントは、反復的な推論、探索、ツール利用を通じて複雑なタスクを解決するが、この過程で長く高コストなコンテキスト履歴が生じうる。論文は、[[SoftwareApplication/openhands]] や [[SoftwareApplication/cursor]] のような最先端のソフトウェアエンジニアリングエージェントがこれに対処するために LLM ベースの要約を用いていることを指摘し、その追加の複雑さが、古い観測を単純に省略する場合と比べて目に見える性能上の利点をもたらすのかを問う。

著者らは、[[SoftwareApplication/swe-agent]] 内で [[Dataset/swe-bench-verified]] を用い、5 つの多様なモデル構成にわたって 2 つのアプローチを体系的に比較し、その知見が OpenHands のエージェントスキャフォールドにも一般化するという初期的な証拠を報告している。その結果、単純な環境の[[DefinedTerm/observation-masking|観測マスキング]]は、素のエージェントに比べてコストを半減させつつ、LLM による要約の解決率と同等、場合によってはわずかに上回ることがわかった。著者らはさらにコストを削減するハイブリッド手法も導入している。

## 要点

- 単純な環境観測マスキング戦略は、素のエージェントに比べてコストを半減させつつ、LLM による要約の解決率と同等、場合によってはわずかに上回る。
- 主要な比較は SWE-agent 内で SWE-bench Verified を用い、5 つのモデル構成にわたって行われている。知見が OpenHands のエージェントスキャフォールドにも当てはまるという証拠は、初期的なものと説明されている。
- 新しいハイブリッド手法は、観測マスキング単独と比べてさらに 7%、LLM による要約単独と比べて 11% コストを削減する。
- 著者らは、この知見が純粋な LLM による要約へと向かう傾向に懸念を投げかけるものであり、効率と有効性のフロンティアにおいてまだ活用されていないコスト削減の余地があることを示していると述べている。

## 補足

この論文は 2025 年 8 月 29 日に arXiv に初投稿された。2025 年 10 月 27 日付のバージョン 3 は、NeurIPS 2025 と併催された第 4 回 DL4C ワークショップ向けのカメラレディ版であり、OpenHands での一般性の検証とハイブリッドなコンテキスト管理戦略が追加されている。著者らは再現性のためにコードとデータを公開している。
