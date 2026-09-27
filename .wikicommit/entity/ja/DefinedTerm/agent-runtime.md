---
title: "エージェントランタイム"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントフレームワーク, エージェントアーキテクチャ, エージェント状態]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-runtime.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM エージェントを本番環境で動かすためのインフラストラクチャ。何よりもまず永続的実行（durable execution）であり、あわせてストリーミング、ヒューマン・イン・ザ・ループのサポート、スレッド内およびスレッドをまたいだ永続化を含む。この用語は LangChain が、エージェントフレームワークの下に位置する層を指して用いており、その例として LangGraph を挙げている。"
---

エージェントランタイムとは、[[BlogPosting/agent-frameworks-runtimes-and-harnesses]] が提案する分類において、
エージェントを本番環境で動かすために必要とされるものである。すなわち、構築のための抽象化ではなく、
インフラストラクチャレベルの関心事を提供するソフトウェアである。この記事を書いた Harrison Chase は、
その主たるものとして永続的実行（durable execution）を挙げ、ストリーミングのサポート、[[DefinedTerm/human-in-the-loop]]
のサポート、スレッドレベルの永続化、スレッド横断の永続化を同じカテゴリーに入れている。LangChain 自身の
例は [[SoftwareApplication/langgraph]] であり、Chase によれば、これは本番運用に耐えるエージェントランタイムとして
ゼロから構築されたものである。彼がこれに最も近いと考えるプロジェクトは、Temporal、Inngest、その他の永続的
実行エンジンである。

## 用法

この記事はランタイムを [[DefinedTerm/agent-framework]] の下に位置づけている。ランタイムは一般に
より低レベルであり、フレームワークを駆動することができる。たとえば LangChain 1.0 は、LangGraph が提供する
ランタイムを活用するために LangGraph の上に構築されている。[[DefinedTerm/agent-harness]] はさらに上、
フレームワークの上に位置する。Chase はこれらの境界が曖昧であると述べており（LangGraph はおそらくランタイムでも
あり、フレームワークでもあると説明するのが最も適切である）、この分類を確立された定義としてではなく、
彼自身による定義の試みとして提示している。

## 関連用語

- [[DefinedTerm/agent-framework]] — ランタイムが駆動しうる抽象化層
- [[DefinedTerm/agent-harness]] — フレームワークの上にある、必要なものが一通りそろった（batteries-included）層
- [[DefinedTerm/human-in-the-loop]] — この記事がランタイムに割り当てている能力の 1 つ
