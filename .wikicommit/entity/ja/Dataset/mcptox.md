---
title: "MCPTox"
type: "schema:Dataset"
lang: ja
tags: [MCP, セキュリティ, ベンチマーク]
translated_from: ".wikicommit/entity/en/Dataset/mcptox.md"
source_commit: "48d80cbbb1b1176580f1d3e42bed65bbe89633ce"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Model Context Protocol サーバー上でのツールポイズニングに対する LLM エージェントの堅牢性を評価するためのベンチマーク。稼働中の実世界の MCP サーバー 45 台と実在のツール 353 個をもとに構築され、10 のリスクカテゴリにわたる 1312 件の悪意あるテストケースで構成される。"
  url: "https://anonymous.4open.science/r/AAAI26-7C02"
---

MCPTox は、[[ScholarlyArticle/mcptox-a-benchmark-for-tool-poisoning-attack-on-real-world-mcp-servers]] で提案されたベンチマークであり、現実的な [[DefinedTerm/model-context-protocol]] の環境において、LLM エージェントが [[DefinedTerm/tool-poisoning]]（ツールのメタデータに埋め込まれた悪意ある指示）に対してどの程度堅牢であるかを評価する。著者らはこれを、この脅威を体系的に評価する初めてのベンチマークと位置づけている。

## 内容

このベンチマークは、稼働中の実世界の MCP サーバー 45 台と実在のツール 353 個をもとに構築されている。10 カテゴリの潜在的リスクを網羅する 1312 件の悪意あるテストケースで構成される。

## 来歴

テストケースは、著者らが設計した 3 種類の異なる攻撃テンプレートから、few-shot 学習によって生成された。論文によれば、データセットは匿名化されたリポジトリで公開されている。

## 利用

[[ScholarlyArticle/mcptox-a-benchmark-for-tool-poisoning-attack-on-real-world-mcp-servers]] は MCPTox を用いて 20 の代表的な LLM エージェント設定を評価し、ツールポイズニングに対する脆弱性が広く見られることを報告している。o1-mini の攻撃成功率は 72.8% に達し、評価したすべてのモデルで拒否率は 3% 未満だった。
