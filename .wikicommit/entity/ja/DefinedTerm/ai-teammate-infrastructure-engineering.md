---
title: "AI Teammate Infrastructure Engineering（ATIE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/ai-teammate-infrastructure-engineering.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、エージェントが必要とするエージェントネイティブなツールチェーンと実行環境 — 人間の認知向けに作られたツールに代わる、機械可読なプロトコル、構造化された診断、セマンティック検索 — を構築するためのエンジニアリング活動。"
---

AI Teammate Infrastructure Engineering（ATIE）は、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提案されている構造化されたエンジニアリング活動の 1 つであり、同論文では「SE for Agents」という括りのもとで [[DefinedTerm/ai-teammate-lifecycle-engineering]]（ATLE）と対になっている。その目的として述べられているのは、エージェントの環境 — [[DefinedTerm/agent-execution-environment]]（AEE） — をエンジニアリングし、エージェントが効果的に動作するために必要なエージェントネイティブなツールチェーンを構築することである。

## 用法

同論文は、人間の開発者向けに作られたツールはエージェントには適さないことが多いと論じる。数十年にわたる SE ツール（IDE、ビジュアルデバッガ）は、エージェントには必要のない認知的過負荷を軽減するものだからである。これにより最適化の目標は、（人間の時間が貴重であるがゆえの）「小さな K に対する precision@K」から、下位のエージェントが結果を後処理できるなら「precision@100」でも許容できる、というものへと移る。同論文は、豊富で建設的なコンパイラメッセージによってエージェントが失敗から素早く学べる Rust のツールチェーンを、エージェントに優しい環境の青写真として挙げ、深く解釈可能なフィードバックを返し、ツール使用の説明をエージェント主導で改善することを支援する、エージェントネイティブな Model Context Protocol（[[DefinedTerm/model-context-protocol]] を参照）サーバーを求めている。その際、Anthropic が自社の MCP の説明を人間ではなくエージェント向けに手作業で最適化したことを、この種の自己改善的なツーリングのループの初期の例として引いている。同論文の ATIE に関する研究ロードマップは、IDE 以後の人間とエージェントのインターフェース（エージェントがより直接的な編集を行うようになるにつれ、オーケストレーション、レビュー、構造化されたメンタリングのためのインターフェースへと向かうもの）や、エージェントのための分散計算基盤（分離、再現性、スケジューリング、コスト管理のためのランタイムサポートで、宣言的な [[DefinedTerm/loopscript]] がワークフローの構造を最適化のために公開するもの）も対象としている。

## 関連用語

[[DefinedTerm/ai-teammate-lifecycle-engineering]], [[DefinedTerm/agent-execution-environment]], [[DefinedTerm/model-context-protocol]]
