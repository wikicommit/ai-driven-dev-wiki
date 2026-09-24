---
title: "Beads"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/beads.md"
source_commit: "ecc1bee15ae3ca4148e95adec43c589c16f912f2"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "Gastown の永続メモリのパターン。エージェントのあらゆる判断とその結果を、完全な来歴とともに記録した、不変で git に裏付けられたレコードであり、ベクトルベースの検索ではなく、タスクグラフと SQL でアドレス可能なデータプレーンを通じて照会される。"
---

Beads は Gastown プロジェクトに由来する永続メモリのパターンであり、エージェントが下すあらゆる判断とその結果を完全な来歴とともに記録した、不変で git に裏付けられたレコードである。この履歴をベクトルデータベースに埋め込みとして格納するのではなく、エージェントはタスクグラフと SQL でアドレス可能なデータプレーンを通じて過去の bead を照会する。これは、フラットな Markdown のメモリファイルに収められる範囲を超えた、構造化され照会可能な組織の記憶として説明されている。

## 用法

これは、マルチエージェントの開発ループを時間とともに賢くしていくための複数の手法の 1 つとして、打ち切り基準を伴うエージェントごとのトークン予算管理や、各タスクの後に `REFLECTION.md` ファイルへ書き出される自己内省の提案と並べて提示されている。

## 関連用語

[[DefinedTerm/ralph-loop]]
