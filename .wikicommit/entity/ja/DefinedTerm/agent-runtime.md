---
title: "エージェントランタイム"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントフレームワーク, エージェントアーキテクチャ, エージェント状態]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-runtime.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM エージェントを本番環境で動かすためのインフラ。何よりもまず耐久実行（durable execution）であり、それに加えてストリーミング、ヒューマン・イン・ザ・ループのサポート、スレッド内およびスレッド横断の永続化を含む。LangChain がエージェントフレームワークの下にある層を指して用いる用語であり、その例として LangGraph が挙げられる。"
---

エージェントランタイムとは、[[BlogPosting/agent-frameworks-runtimes-and-harnesses]] が提案する分類において、エージェントを本番環境で動かすために必要となるもの、すなわち構築のための抽象化ではなく、インフラレベルの考慮事項を提供するソフトウェアである。この投稿を書いた Harrison Chase は、その筆頭に耐久実行（durable execution）を挙げ、ストリーミングのサポート、[[DefinedTerm/human-in-the-loop]] のサポート、スレッドレベルの永続化、スレッド横断の永続化を同じカテゴリーに含めている。LangChain 自身の例は [[SoftwareApplication/langgraph]] であり、Chase はこれが本番対応のエージェントランタイムとしてゼロから構築されたと述べている。彼がこれに最も近いと考えるプロジェクトは、Temporal、Inngest、その他の耐久実行エンジンである。

## 用法

この投稿は、ランタイムを [[DefinedTerm/agent-framework]] の下に位置づけている。ランタイムは一般により低レベルであり、フレームワークを動かす基盤になりうる。たとえば LangChain 1.0 は、LangGraph が提供するランタイムを活用するために LangGraph の上に構築されている。[[DefinedTerm/agent-harness]] はさらにその上、フレームワークの上に位置する。Chase はこれらの境界を曖昧なものだと述べており（LangGraph はおそらくランタイムとフレームワークの両方として説明するのが最も適切だという）、この分類を確立された定義ではなく、定義を与えようとする彼自身の試みとして提示している。

## 関連用語

- [[DefinedTerm/agent-framework]] — ランタイムが基盤となりうる抽象化の層
- [[DefinedTerm/agent-harness]] — フレームワークの上にある、必要なものが一通り揃った（batteries-included）層
- [[DefinedTerm/human-in-the-loop]] — この投稿がランタイムに割り当てる機能の 1 つ
