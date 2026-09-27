---
title: "Claude Squad"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール]
translated_from: ".wikicommit/entity/en/SoftwareApplication/claude-squad.md"
source_commit: "c044ecf40b811dd9fe94970a2c89786a7a0bda4f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Claude を多重化するオープンソースのターミナルアプリケーション。複数の Claude Code インスタンスを起動して別々の tmux ペインで並行して作業させ、開発者がそれぞれに異なるタスクを与えられるようにする。"
  applicationCategory: "マルチエージェントオーケストレーションツール"
---

Claude Squad は、Anthropic の Claude を多重化するオープンソースのターミナルアプリケーションである。複数の
[[SoftwareApplication/claude-code]] インスタンスを起動して別々の tmux ペインで並行して作業させ、開発者がそれぞれに
異なるタスクを渡せるようにする。これを人気のあるツールと説明する
[[BlogPosting/future-of-agentic-coding-conductors-to-orchestrators]] は、[[SoftwareApplication/conductor]] と並べて、
コーディングエージェントを 1 つずつではなく複数同時に並行して実行するために作られたツールの例としてこれを挙げている。

## 機能

その仕組みはホスト型サービスではなくターミナルの多重化である。インスタンスはローカルで、それぞれ独自の tmux ペインで
実行され、開発者はそれぞれに個別に作業を割り当てる。うたわれている利点は並列性である。同記事の表現では、これによって
開発者は並列化により「10 倍速く」コーディングできるとされるが、これは同記事による特徴づけであり、測定された数値では
ない。
