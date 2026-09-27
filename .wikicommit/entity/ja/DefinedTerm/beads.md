---
title: "Beads"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/beads.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Gastown の永続メモリのパターン。エージェントのあらゆる判断とその結果を、完全な来歴付きで、不変かつ git に裏付けられた記録として残し、ベクトルベースの検索ではなく、タスクグラフと SQL でアクセスできるデータプレーンを通じて参照する。"
---

Beads は Gastown プロジェクトに由来する永続メモリのパターンであり、エージェントが下すあらゆる判断とその結果を、完全な来歴を伴う、不変かつ git に裏付けられた記録として残すものである。この履歴をベクトルデータベースに埋め込みとして保存するのではなく、エージェントはタスクグラフと SQL でアクセスできるデータプレーンを通じて過去の bead を参照する。これは、フラットな Markdown のメモリファイルに収まる範囲を超えた、構造化され問い合わせ可能な組織的記憶として説明されている。

## 用法

Beads は、マルチエージェントの開発ループを時間とともに賢くしていくためのいくつかの技法の一つとして提示されており、ほかには、打ち切り基準付きのエージェントごとのトークン予算管理や、各タスクの後に `REFLECTION.md` ファイルに書き出す自己省察の提案がある。

## 関連用語

[[DefinedTerm/ralph-loop]]
