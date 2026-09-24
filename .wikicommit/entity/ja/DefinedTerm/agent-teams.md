---
title: "Agent Teams"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-teams.md"
source_commit: "0426e7f2036ea739db9b2cbdbaaed396066f6d6c"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "真に並列なマルチエージェント実行のための Claude Code の実験的機能。依存関係の追跡とファイルロックを備えた共有タスクリストと、チームメイト同士の直接のピアツーピアのメッセージングを提供し、チームリードがそれらを調整する。"
---

Agent Teams は、複数のエージェントに 1 つのタスクを真に並列で実行させるための Claude Code の実験的機能であり、素のサブエージェント構成には欠けている調整のためのプリミティブを追加する。環境変数 `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` で有効化され、作業を 3 つのレイヤーにわたって構造化する。作業を分解し、タスクリストを作成し、結果を統合する Team Lead。各タスクのステータス（pending、in-progress、completed、blocked）を追跡し、依存関係の追跡とファイルロックを備えた共有タスクリスト。そしてチームメイトである。チームメイトはそれぞれ独自のコンテキストウィンドウを持つ独立した Claude Code インスタンスであり、別々の tmux ペインで動作し、リストから自らタスクを引き受ける。

## 用法

チームメイトはリードを経由せずに互いに直接メッセージをやり取りする。そのため、あるチームメイトがタスクを終えて完了とマークすると、それに依存していたタスクは、リードが仲介役を務めることなく自動的にブロックが解除される。ファイルロックは、2 人のチームメイトが同じファイルを同時に編集することを防ぐ。報告されている実践として、専用の読み取り専用の「@reviewer」チームメイトを起動するというものがある。このチームメイトは lint、テスト、セキュリティスキャンのツールに制限され、タスクが完了するたびに自動的に起動される。これにより、リードは常にレビュー済みのコードだけを統合することになる。

## 関連用語

[[SoftwareApplication/claude-code]], [[DefinedTerm/sub-agent-architecture]]
