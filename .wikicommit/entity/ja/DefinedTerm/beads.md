---
title: "Beads"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/beads.md"
source_commit: "0426e7f2036ea739db9b2cbdbaaed396066f6d6c"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "Gastown の永続メモリのパターン。エージェントのあらゆる判断とその結果を、完全な来歴付きで git に裏打ちされたイミュータブルな記録として残し、ベクトルベースの検索ではなく、タスクグラフと SQL でアドレス可能なデータプレーンを通じて照会する。"
---

Beads は Gastown プロジェクトに由来する永続メモリのパターンであり、エージェントが下すあらゆる判断とその結果を、完全な来歴を伴う、git に裏打ちされたイミュータブルな記録として残す。この履歴をベクトルデータベースの埋め込みとして保存するのではなく、エージェントはタスクグラフと SQL でアドレス可能なデータプレーンを通じて過去の bead を照会する。これは、フラットな markdown のメモリファイルが保持できる範囲を超えた、構造化され照会可能な組織的記憶として説明されている。

## 用法

これは、マルチエージェントの開発ループを時間とともに賢くしていくための複数の手法の 1 つとして提示されており、打ち切り基準を伴うエージェントごとのトークン予算管理や、各タスクの後に `REFLECTION.md` ファイルへ書き出される自己省察の提案と並べられている。

## 関連用語

[[DefinedTerm/ralph-loop]]
