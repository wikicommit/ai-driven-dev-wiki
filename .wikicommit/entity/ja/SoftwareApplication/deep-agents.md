---
title: "Deep Agents"
type: "schema:SoftwareApplication"
lang: ja
aliases: ["DeepAgents"]
tags: [エージェントハーネス, エージェントフレームワーク, エージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/deep-agents.md"
source_commit: "136844949634913857d6d1eb26ef9cb9cfaf8876"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LangChain によるオープンソースパッケージで、開発元はこれをエージェントハーネスに分類している。LangChain の上に構築され、デフォルトのプロンプト、ツール呼び出しの独自方針に基づく処理、計画用のツール、ファイルシステムへのアクセスを追加しており、Claude Code の汎用版と説明されている。"
  applicationCategory: "エージェントハーネス"
  featureList: "デフォルトのプロンプト、ツール呼び出しの独自方針に基づく処理、計画用のツール、ファイルシステムへのアクセス"
  author: "LangChain"
---

Deep Agents（本ページが依拠する記事では「DeepAgents」と表記）は LangChain がメンテナンスするオープンソースパッケージで、
Harrison Chase は [[BlogPosting/agent-frameworks-runtimes-and-harnesses]] の中で、これを同社の最新プロジェクトであり、
人気が高まりつつあるものだと述べている。彼はこれを[[DefinedTerm/agent-harness]]に分類し、
[[DefinedTerm/agent-framework]]である [[SoftwareApplication/langchain]] や、
[[DefinedTerm/agent-runtime]]である [[SoftwareApplication/langgraph]] と区別している。

## 機能

同記事の説明によれば、Deep Agents はエージェントフレームワークよりも高レベルに位置する。LangChain の上に構築され、
デフォルトのプロンプト、ツール呼び出しの独自方針に基づく処理、計画用のツール、ファイルシステムへのアクセスなどを追加している。
Chase の要約では、これは単なるフレームワーク以上のものであり、「バッテリー同梱（batteries included）」で提供される。

このプロジェクトには、LangChain が自社のコーディングエージェントと呼ぶ deepagents-cli も含まれており、Python と
JavaScript で利用できる。[[BlogPosting/improving-deep-agents-with-harness-engineering]] で LangChain は、
モデルを固定したまま、ハーネス――システムプロンプト、ツール、[[DefinedTerm/agent-middleware]]――だけを変更することで、
Terminal Bench 2.0 における deepagents-cli の成績を向上させたと報告している。そこで説明されているミドルウェアは、
開始時にエージェントの作業ディレクトリと利用可能なツールを注入し、同じファイルへの繰り返しの編集を検知し、
終了前にタスクに照らして自分の作業を検証するようエージェントに促す。

## 採用とエコシステム

LangChain は Deep Agents を [[SoftwareApplication/claude-code]] を指して「Claude Code の汎用版（general purpose
version of Claude Code）」とも表現している。同記事はこれを [[SoftwareApplication/claude-agent-sdk]] と並べて論じており、
この SDK を Claude Code 自身がエージェントハーネスへと踏み出した一歩と捉えている。Chase は、この SDK 以外に汎用の
エージェントハーネスは当時それほど多くはなかったと思うと述べつつ、ある意味ではすべてのコーディング CLI が
エージェントハーネスだと主張することもできると認めている。
