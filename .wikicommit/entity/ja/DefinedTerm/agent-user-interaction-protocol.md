---
title: "Agent-User Interaction Protocol（AG-UI）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["AG-UI"]
tags: [エージェント, エージェントプロトコル, ストリーミング]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-user-interaction-protocol.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "エージェントフレームワークとフロントエンドのあいだでミドルウェアとして働くプロトコル。フレームワークの生のイベントを、型付きイベントからなる標準化された Server-Sent Events のストリームに変換することで、フロントエンドがどのフレームワークがそれを生成したかに依存しないようにする。"
---

Agent-User Interaction Protocol（AG-UI）は、AI エージェントをフロントエンドにつなぐためのプロトコルである。[[BlogPosting/developers-guide-to-ai-agent-protocols]] はこれを、エージェントフレームワークの生のイベントを標準化された Server-Sent Events（SSE）のストリームに変換するミドルウェアとして説明している。これによりフロントエンドは、どのエージェントフレームワークがイベントを生成したかを気にすることなく、型付きのイベント — 例として `TEXT_MESSAGE_CONTENT` や `TOOL_CALL_START` が挙げられている — を待ち受けることができる。

## 用法

このガイドが AG-UI を必要とする理由は、エージェントが従来の REST API とどう違うかという点から始まる。REST の呼び出しはレスポンスを返せば終わりだが、エージェントはテキストを少しずつストリーミングし、レスポンスの途中でツールを呼び出し、ときには人間の入力を待つために一時停止する。開発者はこれを直接扱うこともできる。ガイドは、[[SoftwareApplication/agent-development-kit]] がネイティブの `/run_sse` エンドポイントを提供しており、数十行のフロントエンドコードでストリームを解析できると述べている。しかし同時に、その解析コードを、イベント形式が変わるたびに壊れるボイラープレートと呼んでいる。AG-UI はそのボイラープレートを取り除く。

ガイドの例では、ADK のエージェントを `ag_ui_adk` パッケージでラップし、FastAPI アプリのエンドポイントとしてマウントしている。その結果得られるストリームは、実行開始イベントで始まり、各ツール呼び出しを開始・結果・終了のイベントで報告し、テキストを一連のメッセージ内容の差分として配信し、実行終了イベントで閉じる。

ガイドは AG-UI を [[DefinedTerm/agent-to-user-interface-protocol]] と区別している。A2UI は何をレンダリングするかを定義し、AG-UI はそれをどのようにストリーミングするかを定義する。

## 関連用語

- [[DefinedTerm/agent-to-user-interface-protocol]] — ガイドが AG-UI と組み合わせる UI 構成の層
- [[DefinedTerm/human-in-the-loop]] — ガイドが、エージェントのフロントエンドを REST のフロントエンドより難しくしていると述べるエージェントの振る舞いの 1 つである、人間の入力を待つための一時停止
