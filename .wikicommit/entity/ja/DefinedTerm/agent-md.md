---
title: "AGENT.md"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント, エージェント設定, コーディングエージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-md.md"
source_commit: "abe7dbaa9cb573068b927bda52cc565d6ba058e6"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "プロジェクトのルートに置く、ベンダー中立な単一の Markdown ファイルとして提案されたもの。2025 年 7 月に Sourcegraph の Amp チームが打ち出し、各ツール独自の設定ファイルに代わって、あらゆるエージェント型コーディングツールに必要なプロジェクトのコンテキストを与える。"
---

AGENT.md は、ソフトウェアプロジェクトのルートに置く単一の Markdown ファイルのための標準フォーマットとして提案された
ものであり、あらゆるエージェント型コーディングツールに、そのプロジェクトで作業するために必要なコンテキスト —
どのコマンドを実行するか、どの規約に従うか、重要なコードがどこにあるか — を与える。これは 2025 年 7 月付の、
情報提供を目的とした RFC 形式の仕様で定義されており、Geoffrey Huntley が Sourcegraph, Inc. のために執筆し、
`agentmd/agent.md` リポジトリから MIT ライセンスで公開されている。仕様はこのファイルを、開発者がそうでなければ
個別に保守することになるツールごとの設定ファイル — `.cursorrules`、`.windsurfrules`、`.clauderules` など — を
置き換えるものと位置づけ、自らの言葉で「One file, any agent.（1 つのファイルで、どのエージェントにも）」と要約している。

## 用法

仕様はその要件を RFC 2119 の用語で述べている。ファイルはプロジェクトのルートディレクトリに置かなければならず（MUST）、
Markdown を使わなければならない（MUST）。また、プロジェクトの構造と構成、ビルド・テスト・開発のコマンド、コードスタイルと
規約、アーキテクチャと設計パターン、テストのガイドライン、セキュリティ上の考慮事項を扱うべきである（SHOULD）。
実装は階層構造をなす複数のファイル — 全般的なガイダンスのためのルートレベルのファイル、特定のサブシステムのための
サブディレクトリ内のファイル、個人の好みのための `~/.config/AGENT.md` にあるユーザーグローバルなファイル — を
サポートすべきであり（SHOULD）、より具体的なファイルが一般的なファイルに優先する形でそれらをマージすべきである（SHOULD）。
ファイルは `@filename.md` のような `@` メンションを通じて他のファイルを取り込んでもよい（MAY）。

ツールの作り手に対しては、仕様は次のことを求めている。プロジェクトの初期化時にファイルをパースすること、各ツールが
自らのユースケースに関係する設定を抽出すること、ファイルが存在しない場合のフォールバック動作を用意すること、そして
後方互換性のために既存のツール固有の設定ファイルが引き続き機能するようにすること。すでにそうしたファイルを持つ
プロジェクトに対しては、既存のファイルを `AGENT.md` に移動し、元の場所にシンボリックリンクを残す移行コマンドを示している。
これにより、自分のファイル名しか知らないツールも共有ファイルを読むことになる。コマンドは Cline、Claude Code、Cursor、
Firebase Studio、GitHub Copilot、Replit、Windsurf 向けに挙げられており、Gemini CLI、OpenAI Codex、OpenCode 向けには、
`AGENT.md` を既存の `AGENTS.md` にリンクするコマンドになっている。内容についてのガイダンスとしては、新しいチームメンバーが
初日に必要とすること — プロジェクトの概要、ビルドとテストのコマンド、コードスタイル、テスト、セキュリティ、設定 — を
書くことを勧めており、完全なサンプルファイルも含んでいる。

仕様は、Sourcegraph 自身のエージェント型コーディングツールである Amp が 2025 年 5 月 7 日からこのファイルをネイティブに
サポートし、2025 年 7 月 7 日から複数ファイルをサポートしていると記載している。また、
[[SoftwareApplication/claude-code]]、[[SoftwareApplication/cursor]]、Firebase Studio、
[[SoftwareApplication/gemini-cli]]、[[SoftwareApplication/openai-codex]]、
OpenCode、Replit、[[SoftwareApplication/windsurf]] を、ネイティブにではなく上記のシンボリックリンクの仕組みを
通じてサポートしているものとして挙げている。

名前は、複数形の [[DefinedTerm/agents-md]] との争点になっている。仕様によれば、Amp チームは他のエージェント型
コーディングツールの作り手と協力してファイル名の統一に取り組んでいる。単数形を好むのは、agent.md ドメインを所有しており、
それをベンダー中立に保つことを約束しているからだとし — これは当時の AGENTS.md については言えなかったことだと述べている —
一方で、歩み寄る用意があるとも付け加えている。

## 関連用語

- [[DefinedTerm/agents-md]] — 同じ役割を担う、複数形の名前のフォーマット
- [[DefinedTerm/ai-ide-rules]] — AGENT.md が統合しようとしている、ツール固有のルールファイル
