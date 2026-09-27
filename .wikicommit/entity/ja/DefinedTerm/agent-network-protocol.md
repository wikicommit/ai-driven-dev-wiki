---
title: "Agent Network Protocol（ANP）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["ANP"]
tags: [エージェント, エージェントプロトコル, 相互運用性]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-network-protocol.md"
source_commit: "48d80cbbb1b1176580f1d3e42bed65bbe89633ce"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "W3C の分散型識別子（DID）と JSON-LD グラフを用いて、オープンネットワーク上でのエージェントの発見と安全な協調をサポートするエージェント通信プロトコル。2025 年のサーベイで、新たに登場しつつある 4 つのエージェント相互運用プロトコルの 1 つとして説明されている。"
---

Agent Network Protocol（ANP）は、W3C の分散型識別子（DID）と JSON-LD グラフを用いて、オープンネットワーク上でのエージェントの発見と、エージェント間の安全な協調をサポートするエージェント通信プロトコルである。

## 用法

[[ScholarlyArticle/a-survey-of-agent-interoperability-protocols]] は、ANP を LLM 駆動のエージェント間の相互運用性のために新たに登場しつつある 4 つのプロトコルの 1 つとして扱っており、残りは [[DefinedTerm/model-context-protocol]]、[[DefinedTerm/agent-communication-protocol]]、[[DefinedTerm/agent2agent-protocol]] である。このサーベイが提案する段階的な導入ロードマップでは、ANP は最終段階に位置づけられている。ツールアクセスのための MCP、メッセージングのための ACP、協調的なタスク実行のための A2A に続いて、分散型のエージェントマーケットプレイスのために ANP へと導入が広がる。

## 関連用語

- [[DefinedTerm/model-context-protocol]] — サーベイのロードマップにおける最初のプロトコルで、ツールアクセスを担う
- [[DefinedTerm/agent-communication-protocol]] — 構造化された、セッションを意識したメッセージングのためのサーベイ上のプロトコル
- [[DefinedTerm/agent2agent-protocol]] — 協調的なタスク実行のためのサーベイ上のプロトコル
