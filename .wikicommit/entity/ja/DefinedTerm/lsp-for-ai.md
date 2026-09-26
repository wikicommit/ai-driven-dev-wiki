---
title: "LSP for AI"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント型エンジニアリング, ツール利用, MCP]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/lsp-for-ai.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Language Server Protocol によって 1 つの言語サーバーがそれを話すあらゆるエディタで動くようになったのと同じように、AI コーディングツールには開発者ツールとの共通の統合標準が必要だという考え方。"
---

「LSP for AI」とは、Language Server Protocol（LSP）とのアナロジーによって、AI コーディングツールには開発者ツールと統合するための共通標準が必要だとする考え方である。LSP 以前は、あらゆるコードエディタがあらゆるプログラミング言語へのサポートを個別に作り込まなければならなかった。現在では、一度書かれた言語サーバーが LSP を話すどのエディタでも動作し、M×N の統合問題が M+N の問題に変わった。Addy Osmani のエージェント型エンジニアリング用語集は、AI コーディングアシスタントが今日これと同じ M×N 問題に直面しており、それぞれがコードを読み、テストを実行し、ドキュメントを検索するための独自の手段を構築していると述べ、その同等の解決策として、あらゆる AI クライアントがあらゆるツールサーバーと対話できる標準プロトコルを提示している。

## 用法

同用語集は [[DefinedTerm/model-context-protocol]] のようなプロトコルをこのビジョンに向けた初期の一歩として扱い、執筆時点で Anthropic の MCP を最も広く採用されている AI ツールプロトコルと呼んでいる。[[DefinedTerm/ai-coding-agent]] を使って作業するエンジニアにとっての利点として同用語集が挙げるのは、特定の AI ツールへのロックインが減ること — 統合を作り直すことなく AI プロバイダーを乗り換えられること — と、ツール全体の質の向上である。よく作られたサーバー、たとえば GitHub 向けやデータベース向けの MCP サーバーは、単一のクライアントではなく互換性のあるすべてのクライアントに役立つようになるからである。同用語集は、LSP による標準化が高品質な言語ツールの爆発的な増加につながったという対比も示している。

同用語集はこのビジョンをまだ初期段階で発展途上のものと説明しており、分野の成熟に伴って現在のプロトコルが大きく改訂されていくと見込んでいる。

## 関連用語

- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/ai-coding-agent]]
