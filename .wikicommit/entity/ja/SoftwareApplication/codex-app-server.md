---
title: "Codex app-server"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェントハーネス, コーディングエージェント, オープンソース, 人間による監督]
translated_from: ".wikicommit/entity/en/SoftwareApplication/codex-app-server.md"
source_commit: "bcf2a6e3499612efcdde4e63a1d4d23bb9dc9e6f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Codex のエージェントハーネスを、文書化されたクライアントプロトコルを通じて他のアプリケーションに公開する OpenAI のオープンソースコンポーネント。プロダクトは独自のインターフェース、ツール、承認フローを保ったまま、Codex をエージェントループとして動かせる。"
  applicationCategory: "エージェントハーネス統合サーバー"
  featureList: "ローカルの Codex プロセスへの接続、スレッドの作成とターンの開始、イベントのストリーミング、作業の中断、アプリケーションのツールの公開、承認リクエストの処理、永続的な会話"
  author: "[[Organization/openai]]"
---

Codex app-server は、OpenAI が Codex のエージェントハーネス（[[SoftwareApplication/openai-codex]] の Codex アプリ、CLI、IDE 拡張機能を動かしているシステム）を他のアプリケーションに公開するためのコンポーネントである。[[BlogPosting/codex-as-a-platform]] によれば、これはハーネスの機能を文書化されたクライアントプロトコルを通じて提供するもので、アプリケーションはスレッドの作成、ターンの開始、イベントの受信、承認リクエストの処理を行える。OpenAI はこれを Codex CLI および公式の Codex SDK とともにオープンソースとして公開している。

OpenAI の売り込みは、エージェントを必要とするソフトウェアを構築するチームが、新しいランタイムを一から作る代わりに Codex から始め、そのうえで周囲のアプリケーションが何を担うべきかを決められる、というものである。

## 機能

記事の説明によれば、app-server によってアプリケーションは、ローカルの Codex プロセスに接続し、会話を開いたまま維持し、イベントをストリーミングし、作業を中断し、ツールを公開し、承認リクエストに応答できる。その下層では、Codex のハーネスが会話の状態を管理し、実行をストリーミングし、ツールを使用し、設定されたサンドボックスと承認のポリシーを強制し、ターンをまたいで作業を引き継ぐ。

OpenAI はこれを、Codex の上に構築する 3 つの方法の 1 つとして位置づけている。スクリプトや CI タスクのような範囲の限られた非対話型のジョブには `codex exec`、タスクを開始・再開・ストリーミングするプログラム的なワークフローには Codex SDK、そして「エージェントがプロダクトそのものの一部である場合」には app-server である。記事の言葉では、SDK は一般的なプログラム的ワークフローを簡素化する一方、app-server はプロダクトチームにライフサイクルとユーザー体験に対する直接的な制御を与える。

## 採用とエコシステム

OpenAI が説明する役割分担は、アプリケーションがプロダクトのコンテキスト、ビジネスルール、ツール、同意を担い、app-server がエージェントループとサンドボックス化された実行を提供するというものである。その具体例が、OpenAI が app-server 上に構築したサンプルの運用アプリケーション Relay である。架空の出荷ダッシュボードの傍らにエージェントが置かれ、アプリケーション側が所有する MCP ツール（[[DefinedTerm/model-context-protocol]]）に接続されており、出荷を再手配する前には人間の承認を得なければならない。ハーネスがエージェントループ、会話の状態、ストリーミングされるアクティビティ、ツールとのやり取りを扱い、プロダクト側はダッシュボード、記録、制御を保持する。
