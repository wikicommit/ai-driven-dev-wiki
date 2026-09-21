---
title: "Agent Teams"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-teams.md"
source_commit: "09b655594ff0cebcc127385c76c7c935da284a27"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "真の並列マルチエージェント実行のための Claude Code の実験的機能。依存関係の追跡とファイルロックを備えた共有タスクリストと、チームメイトどうしの直接のピアツーピアのメッセージングからなり、チームリードが統率する。"
---

Agent Teams は、1 つのタスクに複数のエージェントを真に並列で走らせるための Claude Code の実験的機能であり、素の
サブエージェント構成には欠けている協調のためのプリミティブを加えるものである。環境変数
`CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` で有効になり、作業を 3 つの層に構造化する。作業を分解し、タスクリストを作り、
結果を統合するチームリード。各タスクのステータス（pending、in-progress、completed、blocked）を、依存関係の追跡と
ファイルロックとともに管理する共有タスクリスト。そして、それぞれが独自のコンテキストウィンドウをもつ独立した Claude Code
のインスタンスであり、別々の tmux ペインで動いて、リストから自らタスクを引き受けるチームメイトである。

## 用法

チームメイトはリードを経由せず互いに直接メッセージを送り合うので、1 人がタスクを終えて完了とマークすると、それに依存して
いたタスクはリードが仲介役として動かなくても自動的にブロック解除される。ファイルロックは、2 人のチームメイトが同じ
ファイルを同時に編集するのを防ぐ。報告されている運用の 1 つは、読み取り専用の「@reviewer」チームメイトを専任で立てること
である。これは lint、テスト、セキュリティスキャンのツールに制限され、タスクが完了するたびに自動的に起動されるので、リード
が統合するのは常にレビュー済みのコードだけになる。

## 関連用語

[[SoftwareApplication/claude-code]], [[DefinedTerm/sub-agent-architecture]]
