---
title: "エージェントフレームワーク"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントフレームワーク, エージェントアーキテクチャ]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-framework.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM エージェントを構築するためのパッケージのうち、主な価値がその抽象化にあるもの。抽象化は世界のメンタルモデルを表し、始めやすくするとともに、開発者に標準的な構築方法を与える。LangChain がこの用語を用いて、そうしたパッケージを、その下にあるエージェントランタイムや上にあるエージェントハーネスと区別している。"
---

エージェントフレームワークとは、[[BlogPosting/agent-frameworks-runtimes-and-harnesses]] が提案する分類において、LLM を使った構築のためのパッケージのうち、主な付加価値が抽象化にあるものを指す。この投稿を書いた Harrison Chase は、そうした抽象化が世界のメンタルモデルを表していると述べる。理想的には、抽象化は始めやすさをもたらし、開発者にアプリケーションを構築する標準的な方法を与えるので、オンボーディングやプロジェクト間の移動が容易になる。彼は LLM を使った構築のためのパッケージの大半をこのように分類しており、LangChain 自身の例として [[SoftwareApplication/langchain]] を挙げ、併せて Vercel の AI SDK、[[SoftwareApplication/crewai]]、[[SoftwareApplication/openai-agents-sdk]]、Google の [[SoftwareApplication/agent-development-kit]]、LlamaIndex を挙げている。

## 用法

この用語は、同じ投稿の中で隣接する 2 つの概念との対比によって定義されている。[[DefinedTerm/agent-runtime]] はフレームワークの下に位置し、耐久実行（durable execution）などの本番環境向けインフラを提供し、フレームワークを動かす基盤になりうる。LangChain 1.0 は LangGraph の上に構築されている。[[DefinedTerm/agent-harness]] はその上に位置し、フレームワークの上にデフォルトのプロンプト、独自の方針に基づくツール呼び出しの処理、計画用ツール、ファイルシステムへのアクセスを加える。Chase は、これらの境界は曖昧であり、明確な定義はまだ存在しないと強調している。たとえば [[SoftwareApplication/langgraph]] は、ランタイムともフレームワークとも呼ばれている。

このカテゴリーに対する根強い批判もまた、抽象化に関するものである。Chase は、出来の悪い抽象化は仕組みを見えにくくし、高度なユースケースに必要な柔軟性を与えないという不満を記している。LangChain のもう 1 つの投稿である [[BlogPosting/agent-middleware]] は、同じ問題をより具体的に述べている。モデル、プロンプト、ツールのリストからなるコアループを中心に構築されたフレームワークは、コンテキストエンジニアリングに対する十分な制御を開発者に与えないため、開発者は自明でないユースケースではいずれも「抽象化から卒業する（graduating off of the abstraction）」ことになる。この投稿の答えは、ループを維持しつつ、[[DefinedTerm/agent-middleware]] を通じてそれを変更可能にすることである。

## 関連用語

- [[DefinedTerm/agent-runtime]] — より低レベルのインフラ層
- [[DefinedTerm/agent-harness]] — より高レベルで、必要なものが一通り揃った層
- [[DefinedTerm/agent-middleware]] — フレームワークのエージェントループをカスタマイズするための LangChain 1.0 の抽象化
- [[DefinedTerm/context-engineering]] — ミドルウェアの投稿が、フレームワークでは得られないとする制御
