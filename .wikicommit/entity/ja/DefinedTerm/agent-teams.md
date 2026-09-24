---
title: "Agent Teams"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-teams.md"
source_commit: "ecc1bee15ae3ca4148e95adec43c589c16f912f2"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "真の並列マルチエージェント実行のための Claude Code の実験的機能。依存関係の追跡とファイルロックを備えた共有タスクリストと、チームメイトどうしの直接のピアツーピア・メッセージングからなり、チームリードがこれを統率する。"
---

Agent Teams は、1 つのタスクに複数のエージェントを真に並列で走らせるための Claude Code の実験的機能であり、素のサブエージェント構成には欠けている協調のためのプリミティブを加えるものである。環境変数 `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` で有効になり、作業を 3 つの層に構造化する。すなわち、作業を分解し、タスクリストを作成し、結果を統合するチームリード。各タスクのステータス（pending、in-progress、completed、blocked）を依存関係の追跡とファイルロックとともに管理する共有タスクリスト。そして、それぞれが独自のコンテキストウィンドウをもつ独立した Claude Code インスタンスとして別々の tmux ペインで動作し、リストから自らタスクを引き受けるチームメイトである。

## 用法

チームメイトはリードを経由せずに互いに直接メッセージを送り合う。そのため、あるチームメイトがタスクを終えて完了とマークすると、それに依存していたタスクは、リードが仲介役を務めることなく自動的にブロック解除される。ファイルロックは、2 人のチームメイトが同じファイルを同時に編集することを防ぐ。報告されている運用の 1 つに、読み取り専用の「@reviewer」チームメイトを専任で立てるというものがある。このチームメイトは lint、テスト、セキュリティスキャンのツールに制限され、タスクが完了するたびに自動的に起動される。これにより、リードが統合するのは常にレビュー済みのコードだけになる。

## 関連用語

[[SoftwareApplication/claude-code]], [[DefinedTerm/sub-agent-architecture]]
