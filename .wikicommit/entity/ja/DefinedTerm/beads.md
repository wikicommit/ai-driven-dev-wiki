---
title: "Beads"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/beads.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Gastown の永続メモリパターン。エージェントのあらゆる判断とその結果を、完全な来歴（provenance）付きで不変かつ Git に裏付けられた記録として残し、ベクトルベースの検索ではなく、タスクグラフと SQL でアドレス指定可能なデータプレーンを通じて照会する。"
---

Beads は Gastown プロジェクトに由来する永続メモリのパターンである。エージェントが下すあらゆる判断とその結果を、完全な来歴（provenance）を伴う、不変で Git に裏付けられた記録として残す。この履歴をベクトルデータベースに埋め込みとして保存するのではなく、エージェントはタスクグラフと SQL でアドレス指定可能なデータプレーンを通じて過去の bead を照会する。これは、フラットな Markdown のメモリファイルに収められる範囲を超えた、構造化され照会可能な組織的記憶と説明されている。

## 用法

これは、マルチエージェントの開発ループを時間とともに賢くしていくためのいくつかの手法の一つとして提示されている。他の手法としては、打ち切り基準を伴うエージェントごとのトークン予算管理や、各タスクの後に `REFLECTION.md` ファイルへ書き出される自己省察の提案が並べられている。

## 関連用語

[[DefinedTerm/ralph-loop]]
