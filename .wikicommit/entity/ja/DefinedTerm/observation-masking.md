---
title: "観測マスキング"
type: "schema:DefinedTerm"
lang: ja
tags: [コンテキスト管理, コーディングエージェント, エージェントの効率]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/observation-masking.md"
source_commit: "48d80cbbb1b1176580f1d3e42bed65bbe89633ce"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM エージェントのためのコンテキスト管理戦略の一つで、LLM による要約でコンテキスト履歴を圧縮する代わりに、古い環境観測をエージェントのコンテキスト履歴から単純に省く。"
---

観測マスキング（observation masking）とは、LLM ベースのエージェントのためのコンテキスト管理戦略であり、履歴を
LLM による要約で圧縮する代わりに、古い環境観測をエージェントのコンテキスト履歴から単純に省くものである。これは、
エージェントが反復的な推論、探索、ツール利用を通じて蓄積する、長くコストのかかるコンテキスト履歴という問題に
対処する。

## 用法

[[ScholarlyArticle/the-complexity-trap]] は観測マスキングを LLM による要約と比較している。後者は、
[[SoftwareApplication/openhands]] や [[SoftwareApplication/cursor]] のような最先端のソフトウェアエンジニアリング
エージェントが用いている手法だと同論文は述べている。[[Dataset/swe-bench-verified]] 上の
[[SoftwareApplication/swe-agent]] において 5 つのモデル構成で比較した結果、同論文は、単純な環境観測のマスキングが
素のエージェントに比べてコストを半減させつつ、LLM による要約と同等、ときにはわずかに上回る解決率を示すことを
見いだした。同論文はさらにハイブリッドな手法も導入しており、これは観測マスキング単独と比べてさらに 7%、
LLM による要約単独と比べて 11% のコスト削減を実現する。

## 適用される場面

この戦略は、反復的なツール利用によって長いコンテキスト履歴を生み出す LLM エージェントに適用され、その根拠は
ソフトウェアエンジニアリングエージェントから得られている。どの程度確立しているかは 1 つの研究の測定結果に依拠
している。上記の比較は SWE-bench Verified 上の SWE-agent で行われたものであり、同論文は、知見が OpenHands の
エージェントスキャフォールドにも一般化するという証拠を初期的なものだと述べている。著者らはこの結果を、純粋な
LLM による要約へと向かう潮流に対して懸念を投げかけるものとして提示している。

## 関連用語

- [[DefinedTerm/compaction]] — エージェントのコンテキストを範囲内に収めるための関連する手法
- [[DefinedTerm/context-engineering]] — エージェントのコンテキストに何が入るかを管理する、より広い実践
