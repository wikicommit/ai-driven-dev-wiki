---
title: "Agent Communication Protocol（ACP）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["ACP"]
tags: [エージェント, エージェントプロトコル, 相互運用性]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-communication-protocol.md"
source_commit: "48d80cbbb1b1176580f1d3e42bed65bbe89633ce"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "RESTful な HTTP 上での汎用的な通信を定めるエージェント通信プロトコル。MIME タイプ付きのマルチパートメッセージと、同期・非同期のやりとりをサポートする。2025 年のサーベイで、新たに登場しつつある 4 つのエージェント相互運用プロトコルの 1 つとして説明されている。"
---

Agent Communication Protocol（ACP）は、RESTful な HTTP 上での汎用的な通信を定めるエージェント通信プロトコルであり、MIME タイプ付きのマルチパートメッセージと、同期・非同期の両方のやりとりをサポートする。[[ScholarlyArticle/a-survey-of-agent-interoperability-protocols]] はその設計を軽量かつランタイム非依存と説明し、それによってスケーラブルなエージェントの呼び出しが可能になるとしている。また、セッション管理、メッセージルーティング、ロールベースの識別子や分散型識別子（DID）との統合をその機能として挙げている。

## 用法

このサーベイは ACP を、LLM で動くエージェント間の相互運用のために新たに登場しつつある 4 つのプロトコルの 1 つとして、[[DefinedTerm/model-context-protocol]]、[[DefinedTerm/agent2agent-protocol]]、[[DefinedTerm/agent-network-protocol]] と並べて扱っている。サーベイが提案する段階的な導入ロードマップでは、ACP は MCP の次に来る。ツールアクセスのために MCP を導入した後、構造化され、マルチモーダルで、セッションを意識したメッセージングのために ACP を導入する。サーベイはこの段階を、スケーラブルな HTTP ベースの配備をまたいだオンラインとオフライン両方のエージェント発見とも結びつけている。

## 関連用語

- [[DefinedTerm/model-context-protocol]] — サーベイのロードマップがツールアクセスのために最初に導入するプロトコル
- [[DefinedTerm/agent2agent-protocol]] — ロードマップが協調的なタスク実行のために加えるプロトコル
- [[DefinedTerm/agent-network-protocol]] — ロードマップが分散型のエージェントマーケットプレイスに向けて拡張していく先のプロトコル
