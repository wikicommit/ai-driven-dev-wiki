---
title: "AGENT.md"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント, エージェント設定, コーディングエージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-md.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "2025 年 7 月に Sourcegraph の Amp チームが提唱した、プロジェクトのルートに置く単一のベンダー中立な Markdown ファイルの提案。各ツール独自の設定ファイルに代わり、あらゆるエージェント型コーディングツールに必要なプロジェクトのコンテキストを与える。"
---

AGENT.md は、ソフトウェアプロジェクトのルートに置かれる単一の Markdown ファイルのための標準フォーマットの提案であり、あらゆるエージェント型コーディングツールに、そのプロジェクトで作業するために必要なコンテキスト — どのコマンドを実行するか、どの規約に従うか、重要なコードがどこにあるか — を与える。これは、2025 年 7 月付の情報提供を目的とした RFC 形式の仕様で定義されており、Geoffrey Huntley が Sourcegraph, Inc. のために執筆し、`agentmd/agent.md` リポジトリから MIT ライセンスで公開されている。この仕様はこのファイルを、開発者が本来ならそれぞれ保守することになるツールごとの設定ファイル — `.cursorrules`、`.windsurfrules`、`.clauderules` など — の代替として位置づけ、それを自らの言葉で「One file, any agent.（1 つのファイルで、あらゆるエージェントに）」と要約している。

## 用法

この仕様は要件を RFC 2119 の用語で述べている。ファイルはプロジェクトのルートディレクトリに置かなければならず（MUST）、Markdown を使わなければならない（MUST）。また、プロジェクトの構造と構成、ビルド・テスト・開発のコマンド、コードスタイルと規約、アーキテクチャと設計パターン、テストのガイドライン、セキュリティ上の考慮事項を扱うべきである（SHOULD）。実装は階層構造をなす複数のファイル — 全般的なガイダンスのためのルートレベルのファイル、特定のサブシステムのためのサブディレクトリ内のファイル、個人の好みのための `~/.config/AGENT.md` にあるユーザー全体のファイル — をサポートすべきであり（SHOULD）、より具体的なファイルが一般的なファイルに優先する形でそれらをマージすべきである（SHOULD）。ファイルは `@filename.md` のような `@` メンションによって他のファイルを取り込んでもよい（MAY）。

ツールの作り手に対して、この仕様は、プロジェクトの初期化時にファイルを解析すること、各ツールが自らの用途に関係する設定を抽出すること、ファイルが存在しない場合のフォールバック動作を用意すること、既存のツール固有の設定ファイルが後方互換性のために引き続き機能することを求めている。すでにそのようなファイルを持つプロジェクトのために、仕様は、既存のファイルを `AGENT.md` に移動し、元の場所にシンボリックリンクを残す移行コマンドを示している。これにより、自分のファイル名しか知らないツールも共有ファイルを読み込める。コマンドは Cline、Claude Code、Cursor、Firebase Studio、GitHub Copilot、Replit、Windsurf について示されており、Gemini CLI、OpenAI Codex、OpenCode については、`AGENT.md` を既存の `AGENTS.md` にリンクするコマンドになっている。内容についてのガイダンスとしては、新しいチームメンバーが初日に必要とすること — プロジェクトの概要、ビルドとテストのコマンド、コードスタイル、テスト、セキュリティ、設定 — を書くことを提案しており、完全なサンプルファイルも含まれている。

この仕様は、Sourcegraph 自身のエージェント型コーディングツールである Amp を、2025 年 5 月 7 日からこのファイルをネイティブにサポートし、2025 年 7 月 7 日から複数ファイルをサポートしているものとして挙げている。また、[[SoftwareApplication/claude-code]]、[[SoftwareApplication/cursor]]、Firebase Studio、[[SoftwareApplication/gemini-cli]]、[[SoftwareApplication/openai-codex]]、OpenCode、Replit、[[SoftwareApplication/windsurf]] を、ネイティブではなく上記のシンボリックリンクの仕組みを通じてサポートしているものとして挙げている。

名前こそが、複数形の [[DefinedTerm/agents-md]] との争点である。仕様によれば、Amp チームは他のエージェント型コーディングツールの作り手と協力してファイル名の統一に取り組んでいる。仕様が単数形を好むのは、agent.md ドメインを所有しており、それをベンダー中立に保つことを約束しているからであり — 仕様によれば、これは当時の AGENTS.md については言えないことだった — そのうえで、歩み寄る用意があるとも付け加えている。

## 関連用語

- [[DefinedTerm/agents-md]] — 同じ役割を担う、複数形の名前のフォーマット
- [[DefinedTerm/ai-ide-rules]] — AGENT.md が統合を提案しているツール固有のルールファイル
