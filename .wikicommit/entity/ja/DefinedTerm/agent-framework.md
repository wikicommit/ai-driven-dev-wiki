---
title: "エージェントフレームワーク"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントフレームワーク, エージェントアーキテクチャ]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-framework.md"
source_commit: "7c488ab4f260fd3eaef2b747c30cbac61c788ca2"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM エージェントを構築するためのパッケージのうち、主な価値がその抽象化にあるもの。抽象化とは世界についてのメンタルモデルであり、着手を容易にし、開発者に標準的な構築方法を与える。LangChain がこの用語を用いて、こうしたパッケージを、その下にあるエージェントランタイムや、その上にあるエージェントハーネスと区別している。"
---

エージェントフレームワークとは、[[BlogPosting/agent-frameworks-runtimes-and-harnesses]] が提案する分類において、LLM を使って構築するためのパッケージのうち、主な付加価値が抽象化にあるものを指す。この投稿を書いた Harrison Chase は、そうした抽象化が世界についてのメンタルモデルを表すものだと説明する。理想的には、抽象化によって着手が容易になり、また開発者にアプリケーションの標準的な構築方法が与えられるため、オンボーディングやプロジェクト間の移動が容易になる。彼は LLM を使って構築するためのパッケージの大半をこのように分類しており、LangChain 自身の例として [[SoftwareApplication/langchain]] を挙げ、並べて Vercel の AI SDK、[[SoftwareApplication/crewai]]、[[SoftwareApplication/openai-agents-sdk]]、Google の [[SoftwareApplication/agent-development-kit]]、LlamaIndex を挙げている。

## 用法

この用語は、同じ投稿に登場する 2 つの隣接概念との対比によって定義されている。[[DefinedTerm/agent-runtime]] はフレームワークの下に位置し、耐久実行（durable execution）のような本番向けインフラを提供するもので、フレームワークを動かす基盤になりうる。LangChain 1.0 は LangGraph の上に構築されている。[[DefinedTerm/agent-harness]] はその上に位置し、フレームワークの上にデフォルトのプロンプト、ツール呼び出しについての明確な方針を持った処理、計画用ツール、ファイルシステムへのアクセスを追加する。Chase は、これらの境界が曖昧であり、明確な定義はまだ存在しないことを強調している。たとえば [[SoftwareApplication/langgraph]] は、ランタイムともフレームワークとも呼ばれている。

このカテゴリーに向けられてきた定番の批判も、抽象化をめぐるものである。Chase は、出来の悪い抽象化は物事の仕組みを見えにくくし、高度なユースケースが必要とする柔軟性を与えない、という不満を記録している。LangChain の別の投稿 [[BlogPosting/agent-middleware]] は、同じ問題をより具体的に述べている。モデル、プロンプト、ツールのリストからなるコアループを中心に構築されたフレームワークは、開発者にコンテキストエンジニアリングに対する十分な制御を与えないため、自明でないユースケースではいずれも、開発者は結局「抽象化から卒業する（graduating off of the abstraction）」ことになる、というのである。この投稿の答えは、ループを維持したまま、それを [[DefinedTerm/agent-middleware]] によって変更可能にすることである。

## 関連用語

- [[DefinedTerm/agent-runtime]] — より低レベルなインフラの層
- [[DefinedTerm/agent-harness]] — より高レベルで、必要なものがあらかじめ揃った（batteries-included）層
- [[DefinedTerm/agent-middleware]] — フレームワークのエージェントループをカスタマイズするための LangChain 1.0 の抽象化
- [[DefinedTerm/context-engineering]] — フレームワークが与えられていないとミドルウェアの投稿が指摘する制御
