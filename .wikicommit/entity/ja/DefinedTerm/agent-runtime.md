---
title: "エージェントランタイム"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントフレームワーク, エージェントアーキテクチャ, エージェント状態]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-runtime.md"
source_commit: "83a69e2424e621789facae2288c4aa54d75ba9ed"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM エージェントを本番環境で動かすためのインフラ。何よりも耐久実行（durable execution）であり、それに加えてストリーミング、ヒューマン・イン・ザ・ループのサポート、スレッド内およびスレッド横断の永続化を含む。LangChain がエージェントフレームワークの下にある層を指して用いる用語で、その例として LangGraph が挙げられる。"
---

エージェントランタイムとは、[[BlogPosting/agent-frameworks-runtimes-and-harnesses]] が提案する分類において、エージェントを本番環境で動かすときに必要となるもの、すなわち構築のための抽象化ではなくインフラレベルの考慮事項を提供するソフトウェアである。この投稿を書いた Harrison Chase は、その筆頭として耐久実行（durable execution）を挙げ、ストリーミングのサポート、[[DefinedTerm/human-in-the-loop]] のサポート、スレッドレベルの永続化、スレッド横断の永続化を同じカテゴリーに入れている。LangChain 自身の例は [[SoftwareApplication/langgraph]] であり、Chase はこれが本番対応のエージェントランタイムとしてゼロから構築されたと述べている。彼がそれに最も近いと考えるプロジェクトは、Temporal、Inngest、その他の耐久実行エンジンである。

## 用法

この投稿はランタイムを [[DefinedTerm/agent-framework]] の下に置いている。ランタイムは一般により低レベルであり、フレームワークを動かす基盤になりうる。LangChain 1.0 は、LangGraph が提供するランタイムを活用するために LangGraph の上に構築されている。[[DefinedTerm/agent-harness]] はさらにその上、フレームワークの上に位置する。Chase はこれらの境界を曖昧なものと述べており（LangGraph はおそらくランタイムとフレームワークの両方と表現するのが最も適切だとしている）、この分類を確立されたものではなく、定義を与えようとする彼自身の試みとして提示している。

## 関連用語

- [[DefinedTerm/agent-framework]] — ランタイムが基盤となりうる抽象化の層
- [[DefinedTerm/agent-harness]] — フレームワークの上にある、必要なものが一通り揃った層
- [[DefinedTerm/human-in-the-loop]] — 投稿がランタイムに割り当てる機能の 1 つ
