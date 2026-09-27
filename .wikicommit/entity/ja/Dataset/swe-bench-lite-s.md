---
title: "SWE-bench Lite-S"
type: "schema:Dataset"
lang: ja
tags: [評価, コーディングエージェント, ソフトウェアエンジニアリング]
translated_from: ".wikicommit/entity/en/Dataset/swe-bench-lite-s.md"
source_commit: "3bb09ff875f75497dbb9ad4d6786745fc33ecce5"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "SWE-bench Lite ベンチマークをフィルタリングしたバージョン。より厳密な評価と比較を可能にするため、Agentless 論文の著者らが、正解パッチが exact である問題や、イシューの記述が不十分または誤解を招く問題を除外して構築した。"
---

SWE-bench Lite-S は、SWE-bench Lite ベンチマークをフィルタリングした派生版であり、ソフトウェアのイシューを解決する
システムをより厳密に評価・比較する目的で構築された。
[[ScholarlyArticle/agentless-demystifying-llm-based-software-engineering-agents]] において、同論文の主要な結果の
測定に用いられた [[DefinedTerm/agentless]] アプローチとともに導入された。

## 内容

このデータセットは、SWE-bench Lite から問題の一部を取り除いたものである。著者らは除外基準を、それらの問題に
見出した欠陥という形で述べている。すなわち、正解パッチが exact であるイシューと、記述が不十分または誤解を招く
イシューである。

## 来歴

フィルタリングは自動処理ではなく、ベンチマークを人手で精査した結果である。Agentless 論文の著者らは、SWE-bench Lite
の問題を手作業で分類し、特定した問題のあるイシューを除外して SWE-bench Lite-S を構築したと報告している。
その動機として述べられているのは、元のベンチマークの欠陥がシステム間の比較で測られる内容に影響するため、
その比較の基盤として代わりにフィルタリング済みのバージョンを提供する、というものである。
