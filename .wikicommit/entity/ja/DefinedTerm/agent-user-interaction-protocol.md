---
title: "Agent-User Interaction Protocol（AG-UI）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["AG-UI"]
tags: [エージェント, エージェントプロトコル, ストリーミング]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-user-interaction-protocol.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "エージェントフレームワークとフロントエンドの間のミドルウェアとして働くプロトコル。フレームワークの生のイベントを型付きイベントの標準化された Server-Sent Events ストリームに変換し、フロントエンドがどのフレームワークがそれを生成したかに依存しないようにする。"
---

Agent-User Interaction Protocol（AG-UI）は、AI エージェントをフロントエンドに接続するためのプロトコルである。
[[BlogPosting/developers-guide-to-ai-agent-protocols]] はこれを、エージェントフレームワークの生のイベントを標準化された
Server-Sent Events（SSE）ストリームに変換するミドルウェアとして説明している。これによりフロントエンドは、どのエージェント
フレームワークがイベントを生成したかを気にすることなく、型付きのイベント——同ガイドの例では `TEXT_MESSAGE_CONTENT` や
`TOOL_CALL_START` など——を待ち受けることができる。

## 用法

同ガイドが AG-UI を必要とする理由として出発点に置くのは、エージェントが従来の REST API とどう異なるかである。REST の呼び出しは
レスポンスを返せば終わりだが、エージェントはテキストを少しずつストリーミングし、応答の途中でツールを呼び出し、ときには
人間の入力を待つために一時停止する。開発者はこれを直接扱うこともできる——同ガイドは、
[[SoftwareApplication/agent-development-kit]] がネイティブの `/run_sse` エンドポイントを提供しており、数十行の
フロントエンドコードでストリームを解析できると述べている——が、その解析コードはイベント形式が変わるたびに壊れる
ボイラープレートだとしている。AG-UI はそのボイラープレートを取り除く。

同ガイドの例では、ADK エージェントを `ag_ui_adk` パッケージでラップし、FastAPI アプリ上のエンドポイントとしてマウントする。
得られるストリームは実行開始イベントで始まり、各ツール呼び出しを開始・結果・終了のイベントで報告し、テキストを一連の
メッセージ内容の差分として届け、実行終了イベントで閉じる。

同ガイドは AG-UI を [[DefinedTerm/agent-to-user-interface-protocol]] と区別している。A2UI は何をレンダリングするかを定義し、
AG-UI はそれをどのようにストリーミングするかを定義する。

## 関連用語

- [[DefinedTerm/agent-to-user-interface-protocol]] — 同ガイドが AG-UI と組み合わせる UI 構成の層
- [[DefinedTerm/human-in-the-loop]] — 同ガイドが、エージェントのフロントエンドを REST のフロントエンドより難しくしている
  と述べるエージェントの振る舞いの一つ（人間の入力を待つための一時停止）
