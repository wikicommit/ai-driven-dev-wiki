---
title: "Agent Communication Protocol（ACP）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["ACP"]
tags: [エージェント, エージェントプロトコル, 相互運用性]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-communication-protocol.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "RESTful HTTP 上での汎用的な通信を定め、MIME タイプ付きのマルチパートメッセージと同期・非同期のやり取りをサポートするエージェント通信プロトコル。2025 年のサーベイで、新たに登場しつつある 4 つのエージェント相互運用プロトコルの 1 つとして説明されている。"
---

Agent Communication Protocol（ACP）は、RESTful HTTP 上での汎用的な通信を定め、MIME タイプ付きのマルチパートメッセージと、同期・非同期両方のやり取りをサポートするエージェント通信プロトコルである。[[ScholarlyArticle/a-survey-of-agent-interoperability-protocols]] はその設計を軽量かつランタイム非依存と説明し、それによってスケーラブルなエージェント呼び出しが可能になるとしている。また、セッション管理、メッセージルーティング、ロールベースの識別子および分散型識別子（DID）との統合を機能として挙げている。

## 用法

このサーベイは ACP を、LLM を用いたエージェント間の相互運用のために新たに登場しつつある 4 つのプロトコルの 1 つとして、[[DefinedTerm/model-context-protocol]]、[[DefinedTerm/agent2agent-protocol]]、[[DefinedTerm/agent-network-protocol]] と並べて扱っている。サーベイが提案する段階的な導入ロードマップでは、ACP は MCP の次に来る。ツールアクセスのために MCP を導入したあと、構造化され、マルチモーダルで、セッションを意識したメッセージングのために ACP を導入する。サーベイはまた、この段階を、スケーラブルな HTTP ベースのデプロイにまたがるオンラインとオフライン両方のエージェント発見とも結びつけている。

## 関連用語

- [[DefinedTerm/model-context-protocol]] — サーベイのロードマップでツールアクセスのために最初に導入されるプロトコル
- [[DefinedTerm/agent2agent-protocol]] — ロードマップで協調的なタスク実行のために追加されるプロトコル
- [[DefinedTerm/agent-network-protocol]] — ロードマップで分散型のエージェントマーケットプレイスのために拡張先となるプロトコル
