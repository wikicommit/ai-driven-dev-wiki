---
title: "エージェントフレームワーク"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントフレームワーク, エージェントアーキテクチャ]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-framework.md"
source_commit: "83a69e2424e621789facae2288c4aa54d75ba9ed"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM エージェントを構築するためのパッケージで、その主な価値が抽象化 — 始めやすくし、開発者に標準的な構築方法を与える、世界についてのメンタルモデル — にあるもの。LangChain はこの用語を、その下にあるエージェントランタイムや、その上にあるエージェントハーネスとこうしたパッケージを区別するために使っている。"
---

エージェントフレームワークとは、[[BlogPosting/agent-frameworks-runtimes-and-harnesses]] が提案する分類において、
LLM を使った構築のためのパッケージのうち、主な付加価値が抽象化にあるものを指す。その記事を書いた Harrison Chase は、
こうした抽象化を世界についてのメンタルモデルを表すものと説明する。理想的には、抽象化は始めやすくし、開発者に
アプリケーションを構築する標準的な方法を与えるので、オンボーディングやプロジェクト間の移動が容易になる。彼は LLM を使った
構築のためのパッケージの大半をこのように分類しており、LangChain 自身の例として [[SoftwareApplication/langchain]] を挙げ、
Vercel の AI SDK、[[SoftwareApplication/crewai]]、[[SoftwareApplication/openai-agents-sdk]]、Google の
[[SoftwareApplication/agent-development-kit]]、LlamaIndex を並べている。

## 用法

この用語は、同じ記事の中で隣接する 2 つの概念との対比によって定義されている。
[[DefinedTerm/agent-runtime]] はフレームワークの下に位置し、耐久実行（durable execution）のような本番用のインフラを
提供し、フレームワークを動かす基盤となりうる — LangChain 1.0 は LangGraph の上に構築されている。
[[DefinedTerm/agent-harness]] はその上に位置し、フレームワークの上にデフォルトのプロンプト、方針の定まった
ツール呼び出しの処理、計画用のツール、ファイルシステムへのアクセスを加える。Chase は、これらの境界は曖昧であり、
明確な定義はまだ存在しないと強調している。たとえば [[SoftwareApplication/langgraph]] は、ランタイムとも
フレームワークとも呼ばれている。

このカテゴリに向けられる根強い批判もまた抽象化に関するものである。Chase は、出来の悪い抽象化は物事の仕組みを
見えにくくし、高度なユースケースに必要な柔軟性を与えない、という不満を記録している。LangChain の 2 つ目の記事
[[BlogPosting/agent-middleware]] は同じ問題をより具体的に述べている。モデル、プロンプト、ツールのリストからなる中核的な
ループを中心に作られたフレームワークは、開発者に [[DefinedTerm/context-engineering]] に対する十分な制御を与えず、
そのため開発者は自明でないユースケースではことごとく「抽象化から卒業する（graduating off of the abstraction）」
ことになる。その記事の答えは、ループを維持したまま、[[DefinedTerm/agent-middleware]] によってそれを変更可能にする
ことである。

## 関連用語

- [[DefinedTerm/agent-runtime]] — より低レベルのインフラ層
- [[DefinedTerm/agent-harness]] — より高レベルの、必要なものが一通りそろった層
- [[DefinedTerm/agent-middleware]] — フレームワークのエージェントループをカスタマイズするための LangChain 1.0 の抽象化
- [[DefinedTerm/context-engineering]] — ミドルウェアの記事が、フレームワークでは得られないと述べる制御
