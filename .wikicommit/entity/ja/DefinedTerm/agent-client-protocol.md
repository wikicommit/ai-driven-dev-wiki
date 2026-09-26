---
title: "Agent Client Protocol（ACP）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["ACP"]
tags: [エージェントプロトコル, コーディングエージェント, コーディングツール]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-client-protocol.md"
source_commit: "5728b89611c82daea3e60f65e72918b701929107"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "IDE やエディタが AI コーディングエージェントとどうやりとりするかを定める標準化された通信プロトコル。IDE はエージェントをサブプロセスとして実行し、そのツール呼び出しの 1 つひとつを把握し制御する。Language Server Protocol になぞらえて、AI エージェントのための LSP と説明されている。"
---

Agent Client Protocol（ACP）は、IDE やエディタと AI コーディングアシスタントとのあいだのやりとりを定める標準化された
通信プロトコルである。[[BlogPosting/acp-protocol-and-multiple-ai-coding-agents]] は、Language Server Protocol を
知っている読者であればこれを「AI エージェントのための LSP」と考えればよいと説明し、その中核的な設計原則として、
エージェントが踏むあらゆるステップを IDE が完全に制御できるようにすることを挙げている。ファイルの読み取り、コードの編集、
コマンドの実行といったあらゆる操作は、IDE から見え、IDE が制御でき、IDE から監査できる明示的なツール呼び出しを
経由しなければならない。

## 用法

この記事が説明するモデルでは、IDE がクライアントとなり、エージェントはサーバーのサブプロセスとして動作し、両者は
標準入出力上の JSON-RPC 2.0 で通信する。セッションは LSP の初期化ハンドシェイクと同様のケイパビリティネゴシエーションから
始まる。エージェントが作業するあいだ、各ステップ — 計画、読み取り中のファイル、これから変更しようとしているコード — は
その都度 IDE にプッシュされる。これには、計画、ツール呼び出しの進捗、思考のチャンク、メッセージのチャンクを運ぶ
`session/update` 通知が使われる。ファイルの変更やコマンドの実行のような機微な操作を行う必要があるとき、エージェントは
IDE に許可を求めなければならず、IDE はユーザーが設定したポリシーに従って自動的に承認するか、ユーザーに尋ねるか、
適用前にレビュー用の差分を表示する。

同じ記事は、セッションの永続化と再開、複数のエージェントモード（`ask`、`code`、`architect`）、
[[DefinedTerm/model-context-protocol]] サーバーのネイティブサポートを機能として挙げている。役割分担については、ACP が
エージェントと IDE のあいだのやりとりを担い、MCP がエージェントの手の届く範囲を外部システムへと広げる、とまとめている。
また、エンタープライズの AI プラットフォームを統制するための 3 層モデルにおいて、ACP を MCP/Skills と
[[DefinedTerm/agent2agent-protocol]] のあいだに位置づけている。

このプロトコルが解決するとされる問題は、LSP が言語について解決したのと同じ問題である。共通の標準がなければ、
あらゆるエディタがあらゆるアシスタントとの統合を実装しなければならず、あらゆるアシスタントがエディタごとにプラグインを
必要とする。その結果、統合コストが上がり、アシスタントが対応できるエディタが限られ、企業はアシスタントの権限、ログ、
利用ポリシーを一元的に管理できなくなる。記事は、コーディングアシスタントを特定のエディタから切り離そうとした
エディタベンダーとして Zed と JetBrains を挙げ、JetBrains をこのプロトコルの主要な推進者の 1 つと呼んでいる。その根拠として、
IDE の中からエージェントをインストールできる公式の ACP Agent Registry と、カスタムエージェントを設定するための
`acp.json` ファイルを挙げている。主要な言語向けの SDK が存在すると報告し、自分たちのチームが公式の Kotlin および
TypeScript の SDK を使って、コーディングツール AutoDev に ACP をクライアントとしてもサーバーとしても統合したことを
説明している。

この記事はまた、このプロトコルをエージェントがブラックボックスであることへの対策として示している。これがなければ、
企業はエージェントがどの機微なファイルにアクセスしたかを監査できず、ユーザーはエージェントが何をしているかを見られず、
IDE は進捗を表示できず、失敗をエージェントの操作までさかのぼって追跡することもできない、と論じている。

## 関連用語

- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agent2agent-protocol]]
- [[DefinedTerm/lsp-for-ai]]
- [[DefinedTerm/agent-communication-protocol]]
