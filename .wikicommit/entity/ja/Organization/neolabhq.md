---
title: "NeoLabHQ"
type: "schema:Organization"
lang: ja
tags: [エージェント, コーディングツール]
translated_from: ".wikicommit/entity/en/Organization/neolabhq.md"
source_commit: "d6b740fcefb776ad598c9c610d08c7220255d861"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Context Engineering Kit の発行元。自社の本番開発の実践から AI コーディングエージェント向けのツールを構築しているソフトウェア開発企業であり、Agent Sandbox コンテナイメージと Agent Eslint Config ルールセットも公開している。"
  url: "https://github.com/NeoLabHQ"
---

NeoLabHQ は、AI コーディングエージェント向けのコンテキストエンジニアリング・プラグインのマーケットプレイスである [[SoftwareApplication/context-engineering-kit]] を公開している GitHub organization である。同社は自らを、開発者が実際の本番プロジェクトに取り組んでいる企業と説明しており、その実践を公開物の源泉として位置づけている。同社によれば、このマーケットプレイスは自社の開発者が長期間にわたって日常的に使ってきたプロンプトに基づいており、キットについて公表している信頼性の数値も、外部のベンチマークではなく、1 年以上にわたる自社開発での利用から得られたものだという。

## 活動と製品

キットに加えて、同組織はキットの補完として位置づける 2 つのプロジェクトを公開しており、いずれも単独でも動作するとしている。

- **Agent Sandbox** — エージェント向けの開発用サンドボックスイメージ。Microsoft 公式の devcontainers イメージを基に構築されており、ほとんどの言語とエージェントでそのまま動作することを意図している。
- **Agent Eslint Config** — 人間ではなく AI エージェント向けに書かれた ESLint 設定。同組織はこれを「過度に主張が強い（overly opinionated）」と呼び、エージェントを複雑度が低く読みやすいコードへと強制するものだと説明している。SonarJS、Unicorn、およびセキュリティと認知的複雑度を対象とした 100 を超えるルールを同梱している。

キットのドキュメントはリポジトリとは別に [neolab.gitbook.io/cek](https://neolab.gitbook.io/cek) で公開されている。
