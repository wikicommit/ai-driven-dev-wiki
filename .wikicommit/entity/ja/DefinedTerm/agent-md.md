---
title: "AGENT.md"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント, エージェント設定, コーディングエージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-md.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "プロジェクトのルートに置く、ベンダー中立な単一の Markdown ファイルの提案。Sourcegraph の Amp チームが 2025 年 7 月に打ち出したもので、各ツール独自の設定ファイルの代わりに、あらゆるエージェント型コーディングツールに必要なプロジェクトのコンテキストを与える。"
---

AGENT.md は、ソフトウェアプロジェクトのルートに置く単一の Markdown ファイルについて提案された標準フォーマットであり、あらゆるエージェント型コーディングツールに、そのプロジェクトで作業するために必要なコンテキスト（どのコマンドを実行するか、どの規約に従うか、重要なコードがどこにあるか）を与える。これは 2025 年 7 月付の情報提供的（informational）な RFC 形式の仕様で定義されており、Geoffrey Huntley が Sourcegraph, Inc. のために執筆し、`agentmd/agent.md` リポジトリから MIT ライセンスの下で公開されている。この仕様は、このファイルを、開発者がそれ以外の場合に個別に維持しているツールごとの設定ファイル（`.cursorrules`、`.windsurfrules`、`.clauderules` など）の代替と位置づけ、自らの言葉で「1 つのファイルで、どのエージェントにも（One file, any agent.）」とまとめている。

## 用法

この仕様は要件を RFC 2119 の用語で述べている。ファイルはプロジェクトのルートディレクトリに置かなければならず（MUST）、Markdown を使わなければならない（MUST）。また、プロジェクトの構造と構成、ビルド・テスト・開発用のコマンド、コードスタイルと規約、アーキテクチャと設計パターン、テストのガイドライン、セキュリティ上の考慮事項を扱うべきである（SHOULD）。実装は、階層構造をなす複数のファイル（全般的なガイダンスのためのルートレベルのファイル、特定のサブシステムのためのサブディレクトリ内のファイル、個人の好みのための `~/.config/AGENT.md` にあるユーザー全体のファイル）をサポートすべきであり（SHOULD）、より具体的なファイルが全般的なファイルに優先する形でそれらをマージすべきである（SHOULD）。ファイルは `@filename.md` のような `@` メンションによって他のファイルを取り込んでもよい（MAY）。

ツールの作り手に対して、この仕様は、ファイルをプロジェクトの初期化時に解析すること、各ツールが自らのユースケースに関係する設定を抽出すること、ファイルが存在しない場合のフォールバック動作を用意すること、そして後方互換性のために既存のツール固有の設定ファイルが引き続き機能することを求めている。すでにそうしたファイルを持つプロジェクト向けには、既存のファイルを `AGENT.md` に移動し、元の場所にシンボリックリンクを残す移行コマンドを示しており、自分のファイル名しか知らないツールでも共有ファイルを読めるようにしている。コマンドは Cline、Claude Code、Cursor、Firebase Studio、GitHub Copilot、Replit、Windsurf 向けに示されており、Gemini CLI、OpenAI Codex、OpenCode 向けのコマンドは `AGENT.md` を既存の `AGENTS.md` にリンクする。内容についてのガイダンスとしては、新しいチームメンバーが初日に必要とするもの（プロジェクトの概要、ビルドとテストのコマンド、コードスタイル、テスト、セキュリティ、設定）を書くことを提案しており、完全なサンプルファイルも含んでいる。

この仕様は、Sourcegraph 自身のエージェント型コーディングツールである Amp を、2025 年 5 月 7 日からこのファイルを、2025 年 7 月 7 日から複数ファイルをネイティブにサポートしているものとして挙げている。そして [[SoftwareApplication/claude-code]]、[[SoftwareApplication/cursor]]、Firebase Studio、[[SoftwareApplication/gemini-cli]]、[[SoftwareApplication/openai-codex]]、OpenCode、Replit、[[SoftwareApplication/windsurf]] を、ネイティブにではなく、上記のシンボリックリンクの仕組みを通じてサポートしているものとして挙げている。

名前は、複数形の [[DefinedTerm/agents-md]] との争点である。この仕様によれば、Amp チームは他のエージェント型コーディングツールの作り手と協力してファイル名の統一に取り組んでおり、単数形を好むのは agent.md ドメインを保有しており、それをベンダー中立に保つことを約束しているからだという。これは当時の AGENTS.md については言えなかったことだとしつつ、妥協する用意もあると付け加えている。

## 関連用語

- [[DefinedTerm/agents-md]] — 同じ役割を担う、複数形の名前のフォーマット
- [[DefinedTerm/ai-ide-rules]] — AGENT.md が統合を提案している、ツール固有のルールファイル
