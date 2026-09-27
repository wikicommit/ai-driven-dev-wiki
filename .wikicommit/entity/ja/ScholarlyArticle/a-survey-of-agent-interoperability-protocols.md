---
title: "エージェント相互運用性プロトコルのサーベイ：Model Context Protocol（MCP）、Agent Communication Protocol（ACP）、Agent-to-Agent Protocol（A2A）、Agent Network Protocol（ANP）"
type: "schema:ScholarlyArticle"
lang: ja
tags: [エージェント, エージェントプロトコル, マルチエージェント, 相互運用性]
review_status: pending
translated_from: ".wikicommit/entity/en/ScholarlyArticle/a-survey-of-agent-interoperability-protocols.md"
source_commit: "48d80cbbb1b1176580f1d3e42bed65bbe89633ce"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM を基盤とするエージェントのための 4 つの新興通信プロトコル（MCP、ACP、A2A、ANP）を取り上げ、インタラクションモード、ディスカバリーの仕組み、通信パターン、セキュリティモデルの観点で比較し、段階的な採用ロードマップを提案する 2025 年の arXiv サーベイ。"
  author: ["Abul Ehtesham", "Aditi Singh", "Gaurav Kumar Gupta", "Saket Kumar"]
  datePublished: "2025-05-04"
  keywords: ["エージェントの相互運用性", "Model Context Protocol", "Agent Communication Protocol", "Agent-to-Agent Protocol", "Agent Network Protocol"]
---

このサーベイの出発点は、大規模言語モデルを基盤とする自律エージェントには、ツールを統合し、コンテキストデータを共有し、異種システムをまたいでタスクを調整するための堅牢で標準化されたプロトコルが必要だという主張である。場当たり的な統合は、スケールさせること、安全にすること、領域をまたいで汎用化することが難しいからだ。本論文は、それぞれ異なるデプロイ文脈で相互運用性に取り組む 4 つの新興エージェント通信プロトコル、すなわち [[DefinedTerm/model-context-protocol]]（MCP）、[[DefinedTerm/agent-communication-protocol]]（ACP）、[[DefinedTerm/agent2agent-protocol]]（A2A）、[[DefinedTerm/agent-network-protocol]]（ANP）を検討している。

論文は 4 つのプロトコルをインタラクションモード、ディスカバリーの仕組み、通信パターン、セキュリティモデルの観点で比較し、その比較に基づいて段階的な採用ロードマップを提案する。まずツールアクセスのために MCP、次に構造化・マルチモーダルでセッションを意識したメッセージングのために ACP、続いて協調的なタスク実行のために A2A、最後に分散型のエージェントマーケットプレイスのために ANP という順序である。著者らはこの研究を、LLM を基盤とするエージェントの安全で相互運用可能かつスケーラブルなエコシステムを設計するための基盤として位置づけている。

## 主なポイント

- MCP は、安全なツール呼び出しと型付きデータ交換のための JSON-RPC ベースのクライアント・サーバーインターフェースを提供する。
- ACP は、RESTful HTTP 上の汎用通信プロトコルを定義し、MIME タイプ付きのマルチパートメッセージと、同期・非同期の両方のインタラクションをサポートする。
- A2A は、能力ベースの Agent Card を用いたピアツーピアのタスク委譲を可能にし、企業のエージェントワークフローをまたいだ協調を支える。
- ANP は、W3C の分散型識別子（DID）と JSON-LD グラフを用いて、オープンネットワーク上でのエージェントのディスカバリーと安全な協調をサポートする。
- 各プロトコルは、インタラクションモード、ディスカバリーの仕組み、通信パターン、セキュリティモデルの観点で比較されている。
- 提案される採用ロードマップは段階的である。ツールアクセスのための MCP から始め、ACP、A2A と進み、最後に分散型エージェントマーケットプレイスのための ANP に至る。

## 補足

本論文は 2025 年 5 月 4 日に arXiv へ初めて投稿され、2025 年 5 月 23 日に改訂された（バージョン 2）。分類は Artificial Intelligence（cs.AI）である。
