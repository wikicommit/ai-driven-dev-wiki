---
title: "AI Teammate Infrastructure Engineering（ATIE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
translated_from: ".wikicommit/entity/en/DefinedTerm/ai-teammate-infrastructure-engineering.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Structured Agentic Software Engineering（SASE）で提唱されている、エージェントが必要とするエージェントネイティブなツールチェーンと実行環境を構築するためのエンジニアリング活動。人間の認知向けに作られたツールに代えて、機械可読なプロトコル、構造化された診断、セマンティック検索を提供する。"
---

AI Teammate Infrastructure Engineering（ATIE）は、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提唱されている構造化されたエンジニアリング活動の 1 つであり、同論文では「SE for Agents」という括りのもとで [[DefinedTerm/ai-teammate-lifecycle-engineering]]（ATLE）と対になっている。その目的は、エージェントの環境、すなわち [[DefinedTerm/agent-execution-environment]]（AEE）をエンジニアリングし、エージェントが効果的に動作するために必要なエージェントネイティブなツールチェーンを構築することだとされている。

## 用法

同論文は、人間の開発者向けに作られたツールはしばしばエージェントには適さないと論じる。数十年にわたる SE ツール（IDE、ビジュアルデバッガ）は、エージェントには不要な認知的過負荷を軽減するためのものだからである。これにより最適化の目標は、（人間の時間は貴重なので）「小さな K に対する precision@K」から、下位のエージェントが結果を後処理できる場合には「precision@100」でも許容できる、というものへと移る。同論文は、豊富で建設的なコンパイラメッセージによってエージェントが失敗から素早く学べる Rust のツールチェーンを、エージェントにとって扱いやすい環境の青写真として挙げている。また、深く解釈可能なフィードバックを返し、ツール利用の説明をエージェント主導で改良できるようにする、エージェントネイティブな Model Context Protocol（[[DefinedTerm/model-context-protocol]] を参照）サーバーを求めており、この種の自己改善的なツーリングループの初期の例として、Anthropic が自社の MCP の説明を人間ではなくエージェント向けに手作業で最適化したことを挙げている。同論文の ATIE に関する研究ロードマップは、IDE 以後の人間とエージェントのインターフェース（エージェントがより多くの編集を直接行うようになるにつれ、オーケストレーション、レビュー、構造化されたメンタリングのためのインターフェースへと移行すること）や、エージェントのための分散計算基盤（分離、再現性、スケジューリング、コスト管理のための実行時サポートで、宣言的な [[DefinedTerm/loopscript]] によってワークフローの構造を最適化のために公開するもの）も対象としている。

## 関連用語

[[DefinedTerm/ai-teammate-lifecycle-engineering]]、[[DefinedTerm/agent-execution-environment]]、[[DefinedTerm/model-context-protocol]]
