---
title: "Beads"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/beads.md"
source_commit: "c6bf44a9d0262400c75a0abf7dee6a8fbb53ff80"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "Gastown の永続メモリのパターン。エージェントのあらゆる判断とその結果を、完全な来歴付きで、不変かつ git に裏付けられた記録として残し、ベクトルベースの検索ではなく、タスクグラフと SQL でアドレス指定可能なデータプレーンを通じて照会する。"
---

Beads は Gastown プロジェクトに由来する永続メモリのパターンであり、エージェントが下すあらゆる判断とその結果を、完全な来歴を伴う不変かつ git に裏付けられた記録として残すものである。この履歴をベクトルデータベースに埋め込みとして保存するのではなく、エージェントはタスクグラフと SQL でアドレス指定可能なデータプレーンを通じて過去の bead を照会する。これは、フラットな Markdown のメモリファイルが保持できる範囲を超えた、構造化され照会可能な組織の記憶として説明されている。

## 用法

これは、マルチエージェントの開発ループを時間とともに賢くするためのいくつかの手法の 1 つとして示されている。ほかには、停止基準を伴うエージェントごとのトークン予算の設定や、各タスクの後に `REFLECTION.md` ファイルへ書き出される自己省察の提案がある。

## 関連用語

[[DefinedTerm/ralph-loop]]
