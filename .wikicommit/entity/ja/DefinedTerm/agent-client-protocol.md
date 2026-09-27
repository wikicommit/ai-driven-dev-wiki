---
title: "Agent Client Protocol（ACP）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["ACP"]
tags: [エージェントプロトコル, コーディングエージェント, コーディングツール]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-client-protocol.md"
source_commit: "5728b89611c82daea3e60f65e72918b701929107"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "IDE やエディタが AI コーディングエージェントとどのようにやり取りするかを定める標準化された通信プロトコル。IDE はエージェントをサブプロセスとして実行し、そのツール呼び出しの一つひとつを把握・制御する。Language Server Protocol になぞらえて「AI エージェントのための LSP」と説明される。"
---

Agent Client Protocol（ACP）は、IDE やエディタと AI コーディングアシスタントとのあいだのやり取りを定める、標準化された通信プロトコルである。[[BlogPosting/acp-protocol-and-multiple-ai-coding-agents]]
は、Language Server Protocol を知っている読者なら「AI エージェントのための LSP」と考えればよいものだと説明し、その中心的な設計原則として、エージェントが踏むあらゆるステップを IDE が完全に制御できるようにすることを挙げている。ファイルの読み込み、コードの編集、コマンドの実行といったあらゆる操作は、IDE から見え、IDE が制御でき、IDE から監査できる明示的なツール呼び出しを経由しなければならない。

## 用法

この投稿が説明するモデルでは、IDE がクライアントとなり、エージェントはサーバーのサブプロセスとして動作し、両者は標準入出力上の JSON-RPC 2.0 で通信する。セッションは、LSP の初期化ハンドシェイクに似たケイパビリティネゴシエーションから始まる。エージェントが作業しているあいだ、各ステップ——計画、読み込み中のファイル、これから変更しようとしているコード——は、発生したその場で IDE へプッシュされる。これは、計画、ツール呼び出しの進捗、思考のチャンク、メッセージのチャンクを運ぶ `session/update` 通知を通じて行われる。ファイルの変更やコマンドの実行といったセンシティブな操作を行う必要があるとき、エージェントは IDE に許可を求めなければならない。IDE は、ユーザーが設定したポリシーに従って自動的に承認するか、ユーザーに確認するか、適用前にレビュー用の差分を表示することができる。

同じ投稿は、セッションの永続化と再開、複数のエージェントモード（`ask`、`code`、`architect`）、[[DefinedTerm/model-context-protocol]] サーバーのネイティブサポートを機能として挙げている。役割分担については、ACP がエージェントと IDE のあいだのやり取りを担い、MCP がエージェントの手を外部システムへと広げる、とまとめている。また、エンタープライズ AI プラットフォームを統制するための 3 層モデルの中で、ACP を MCP/Skills と [[DefinedTerm/agent2agent-protocol]] のあいだに位置づけている。

このプロトコルが解決するとされる問題は、LSP が言語について解決した問題と同じである。共通の標準がなければ、各エディタはアシスタントごとに統合を実装しなければならず、各アシスタントもエディタごとにプラグインを必要とする。その結果、統合コストが上がり、アシスタントが対応できるエディタが限られ、企業はアシスタントの権限、ログ、利用ポリシーを一か所で管理できなくなる。投稿は、コーディングアシスタントを特定のエディタから切り離すことに乗り出したエディタベンダーとして Zed と JetBrains を挙げ、JetBrains をこのプロトコルの主要な推進者の 1 つと呼んでいる。その根拠として、IDE の中からエージェントをインストールできる公式の ACP Agent Registry と、カスタムエージェントを設定するための `acp.json` ファイルを挙げている。主要な言語向けに SDK が存在すると報告しており、自チームが公式の Kotlin SDK と TypeScript SDK を使って、コーディングツール AutoDev に ACP をクライアントとサーバーの両方として統合したことも述べている。

投稿はさらに、このプロトコルを、エージェントがブラックボックスであるという問題への対策としても提示している。これがなければ、企業はエージェントがどのセンシティブなファイルにアクセスしたかを監査できず、ユーザーはエージェントが何をしているのかを見られず、IDE は進捗を表示できず、障害をエージェントの操作までさかのぼって追跡することもできない、と論じている。

## 関連用語

- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agent2agent-protocol]]
- [[DefinedTerm/lsp-for-ai]]
- [[DefinedTerm/agent-communication-protocol]]
