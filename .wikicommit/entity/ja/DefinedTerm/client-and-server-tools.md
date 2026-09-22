---
title: "クライアントツールとサーバーツール"
type: "schema:DefinedTerm"
lang: ja
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/client-and-server-tools.md"
source_commit: "a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"
tags: [ツール利用, エージェントアーキテクチャ, LLM]

properties:
  description: "Anthropic の Claude API における、呼び出し側のアプリケーション内でコードが走るツールと、プロバイダ自身のインフラ上で走るツールの区別。ツールが異なる第一の軸である。"
---

クライアントツールとサーバーツールは、Anthropic の Claude API が区別する 2 種類のツールであり、ツールのコードが実際に
どこで実行されるかによって分けられる。Anthropic のドキュメントは、ツールは主としてこの軸に沿って異なると述べている。
クライアントツールは呼び出し側のアプリケーション内で走る。モデルは `stop_reason: "tool_use"` と 1 つ以上の `tool_use`
ブロックで応答し、アプリケーション自身のコードがその操作を実行し、結果を `tool_result` ブロックで返す。サーバーツールは
Anthropic のインフラ上で走るので、呼び出し側はハンドラを一切書かずに結果を直接受け取る——ドキュメントは最小の例として
ウェブ検索を挙げており、そこでは検索が Anthropic 側で走り、引用付きの結果が同じレスポンスの中で返ってくる。

## 用法

Anthropic のドキュメントは、提供するツールをこの線に沿って 3 つのカテゴリに分類している——うち 2 つはクライアント側、
1 つはサーバー側である。*自前のツール*は、開発者がスキーマを書いて定義し、アプリケーションが各呼び出しを実行するもので
ある。*Anthropic スキーマのクライアントツール*は、Anthropic がスキーマを公開しモデルをそれに合わせて訓練しているもので、
呼び出しの実行と `tool_result` の返却は依然としてアプリケーションが行う——memory、bash、text editor、computer use、
browser use の各ツールがこれにあたる。*サーバーツール*はハンドラのコードをまったく必要としない——web search、web fetch、
code execution、advisor ツール、tool search ツール、そして MCP コネクタがこれにあたる。

この分離は、文書化されている一つのケースにおいては絶対的ではない。ドキュメントは、サーバーツールの結果が直接返されるのは、
モデルがそれを呼び出し側のクライアントツールと同じ並列ツール呼び出しのグループの中で呼ばない場合に*限る*と注記している。

ツールがどこで走るかは、課金のされ方も決める。Anthropic は、クライアント側のツールは他の API リクエストと同じ価格である
一方、サーバー側のツールはトークンに加えて利用量に基づく追加料金が発生しうると述べている。その例は、実行した検索ごとに
課金されるウェブ検索である。

## 関連用語

- [[DefinedTerm/tool-use-design-pattern]] — この区別が精密化している一般的なパターン
- [[DefinedTerm/computer-use]] — Anthropic スキーマのクライアントツールの一つ
- [[DefinedTerm/model-context-protocol]] — エージェントが外部ツールに到達する別の経路
- [[DefinedTerm/code-execution-mcp]] — エージェントに代わってコードを走らせる関連するアプローチ
