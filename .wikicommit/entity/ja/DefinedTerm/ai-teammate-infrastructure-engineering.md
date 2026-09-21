---
title: "AI Teammate Infrastructure Engineering（ATIE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/ai-teammate-infrastructure-engineering.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）が提唱する、エージェントが必要とするエージェントネイティブなツールチェーンと実行環境を構築するためのエンジニアリング活動。人間の認知に合わせて作られたツールに代えて、機械可読なプロトコル、構造化された診断、意味的な検索を据える。"
---

AI Teammate Infrastructure Engineering（ATIE）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] が [[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提唱する、構造化されたエンジニアリング活動の 1 つであり、そこでは「エージェントのための SE」という括りのもとで [[DefinedTerm/ai-teammate-lifecycle-engineering]]（ATLE）と対をなしている。その目的として掲げられているのは、エージェントの環境 — [[DefinedTerm/agent-execution-environment]]（AEE）— を設計し、エージェントが効果的に働くために必要な、エージェントネイティブなツールチェーンを構築することである。

## 用法

論文は、人間の開発者向けに作られたツールがエージェントにはしばしば適さないと論じる。何十年にもわたる SE のツール（IDE、ビジュアルデバッガ）は、エージェントには不要な認知的過負荷を減らすためのものだからである。そこで最適化の目標は、「小さな K に対する precision@K」（人間の時間は貴重だからである）から、下位のエージェントが結果を後処理できるなら「precision@100」でも許容される、というものへと移る。論文は Rust のツールチェーン — その豊かで建設的なコンパイラのメッセージは、エージェントが失敗から素早く学ぶことを可能にする — を、エージェントに優しい環境の設計図として指し示す。そして、深く解釈可能なフィードバックを返し、ツールの利用方法の記述をエージェント自身が洗練させられるようにする、エージェントネイティブな Model Context Protocol（[[DefinedTerm/model-context-protocol]] を参照）のサーバーを求めている。その際、Anthropic が自社の MCP の記述を人間向けではなくエージェント向けに手作業で最適化したことを、この種の自己改善するツールのループの初期の例として引いている。ATIE についての論文の研究ロードマップは、IDE 以後の人間とエージェントのインターフェース（エージェントがより直接的な編集を担うようになるにつれて、オーケストレーション・レビュー・構造化された指導のためのインターフェースへと向かうこと）と、エージェントのための分散計算基盤（隔離・再現性・スケジューリング・コスト制御のランタイム上の支援と、最適化のためにワークフローの構造を露わにする宣言的な [[DefinedTerm/loopscript]]）も覆っている。

## 関連用語

[[DefinedTerm/ai-teammate-lifecycle-engineering]]、[[DefinedTerm/agent-execution-environment]]、[[DefinedTerm/model-context-protocol]]
