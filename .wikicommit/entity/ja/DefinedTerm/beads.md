---
title: "Beads"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/beads.md"
source_commit: "09b655594ff0cebcc127385c76c7c935da284a27"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Gastown の永続的記憶パターン。エージェントのあらゆる意思決定と結果を、完全な来歴とともに、イミュータブルかつ git に裏づけられた記録として残し、ベクトルベースの検索ではなくタスクグラフと SQL でアドレス指定可能なデータプレーンを通して問い合わせる。"
---

Beads とは、Gastown プロジェクトに由来する永続的記憶のパターンである。エージェントが下したあらゆる意思決定とその結果を、完全な来歴を伴った、イミュータブルかつ git に裏づけられた記録として残す。この履歴をベクトルデータベースに埋め込みとして保存するのではなく、エージェントは過去の bead をタスクグラフと SQL でアドレス指定可能なデータプレーンを通して問い合わせる。これは、平坦な Markdown の記憶ファイルが保持しうる範囲を超えた、構造化され問い合わせ可能な組織的記憶として説明されている。

## 使われ方

これは、マルチエージェントの開発ループを時間とともに賢くしていくためのいくつかの技法のひとつとして提示されており、打ち切り基準を伴うエージェントごとのトークン予算管理や、各タスクの後に `REFLECTION.md` ファイルへ書き出される自己省察の提案と並べて挙げられている。

## 関連用語

[[DefinedTerm/ralph-loop]]
