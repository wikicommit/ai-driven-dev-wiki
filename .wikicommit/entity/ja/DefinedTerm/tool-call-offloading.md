---
title: "ツール呼び出しのオフロード"
type: "schema:DefinedTerm"
lang: ja
tags: [コンテキストエンジニアリング, ハーネスエンジニアリング, コンテキストウィンドウ]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/tool-call-offloading.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "大きなツール出力のうち先頭と末尾だけをエージェントのコンテキストに残し、出力全体をファイルシステムに書き出して、必要に応じてモデルが読めるようにするハーネスの手法。"
---

ツール呼び出しのオフロードとは、大きなツール出力がエージェントのコンテキストウィンドウに及ぼす影響を抑えるためのハーネスの手法である。ツールの出力が閾値のトークン数を超えた場合、ハーネスはその出力の先頭と末尾のトークンだけをコンテキストに残し、出力全体をファイルシステムにオフロードして、必要であればモデルが引き続きアクセスできるようにする。LangChain の [[BlogPosting/the-anatomy-of-an-agent-harness]] は、これを、有用な情報をもたらさないままノイズとしてコンテキストウィンドウを散らかす出力の影響を減らす方法として説明している。

## 用法

この用語は [[DefinedTerm/harness-engineering]] において、ハーネスが [[DefinedTerm/context-rot]]（コンテキストが埋まるにつれてモデルの推論とタスク完遂の能力が劣化すること）に対して適用する戦略の 1 つとして用いられる。同じ記事はこれを、ウィンドウがほぼ満杯になったときに既存のコンテキストを要約してオフロードする [[DefinedTerm/compaction]]、そして [[DefinedTerm/progressive-disclosure]] を用いて開始時にすべてのツールを読み込むことを避ける Skills と並べて扱っている。この手法はエージェントが読み取れるファイルシステムを前提としており、同記事はファイルシステムを最も基礎的なハーネスのプリミティブとして扱っている。

## 関連用語

- [[DefinedTerm/context-rot]]
- [[DefinedTerm/compaction]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/progressive-disclosure]]
