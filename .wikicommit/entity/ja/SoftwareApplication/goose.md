---
title: "goose"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングエージェント, オープンソース, CLI, MCP]
translated_from: ".wikicommit/entity/en/SoftwareApplication/goose.md"
source_commit: "abe7dbaa9cb573068b927bda52cc565d6ba058e6"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "ユーザー自身のマシン上でデスクトップアプリ、CLI、組み込み可能な API として動作するオープンソースの汎用 AI エージェント。コーディングに加え、調査、執筆、自動化、データ分析にも使え、Model Context Protocol を通じて拡張機能と接続する。"
  applicationCategory: "AI エージェント"
  operatingSystem: "macOS, Linux, Windows"
---

goose は、Apache 2.0 ライセンスのもとで公開されている、ユーザー自身のマシン上で動作するオープンソースの AI エージェントで
ある。その README は、これをコーディングツールにとどまらない汎用のものとして提示しており —— 「コード、ワークフロー、そして
その間にあるあらゆるもののために」 —— 、コードと並んで調査、執筆、自動化、データ分析を用途として挙げている。リポジトリの
説明はさらに、コードの提案にとどまらず、任意の LLM を使ってインストール、実行、編集、テストまで行うと付け加えている。この
プロジェクトは Linux Foundation の Agentic AI Foundation（AAIF）の一部であり、そのリポジトリは GitHub の `aaif-goose`
組織のもとで公開されている。

## 機能

goose には 3 つの形態がある。macOS、Linux、Windows 向けのネイティブなデスクトップアプリ、ターミナルでのワークフローの
ための完全な CLI、そして他の場所に組み込むための API である。Rust で書かれており、README はそれによって性能と可搬性が
得られているとしている。

特定のモデルに依存しない。README によれば、15 以上のプロバイダーで動作し、その中には Anthropic、OpenAI、Google、Ollama、
OpenRouter、Azure、Bedrock が含まれる。また、API キーを使うことも、ACP を通じてユーザーの既存の Claude、ChatGPT、Gemini
のサブスクリプションを使うこともできる。その機能は [[DefinedTerm/model-context-protocol]] を通じて拡張される。README は、
このオープン標準を介して 70 以上の拡張機能と接続できると述べている。

## 採用とエコシステム

標準ビルドのほかに、プロジェクトはカスタムディストリビューション —— プロバイダー、拡張機能、ブランディングをあらかじめ
設定した goose のビルド —— について文書化しており、プロジェクトのガバナンス文書も公開している。
