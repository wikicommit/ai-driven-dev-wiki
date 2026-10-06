---
title: "MCPTox: 実世界の MCP サーバーに対するツールポイズニング攻撃のベンチマーク"
type: "schema:ScholarlyArticle"
lang: ja
tags: [MCP, セキュリティ, エージェント, ベンチマーク]
review_status: reviewed
translated_from: ".wikicommit/entity/en/ScholarlyArticle/mcptox-a-benchmark-for-tool-poisoning-attack-on-real-world-mcp-servers.md"
source_commit: "48d80cbbb1b1176580f1d3e42bed65bbe89633ce"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "現実的な Model Context Protocol の環境において、ツールポイズニングに対する LLM エージェントの堅牢性を体系的に評価する初のベンチマークと自ら位置づける MCPTox を紹介し、20 の LLM エージェント設定にわたって脆弱性が広く見られることを報告した 2025 年の arXiv 論文。"
  author: ["Zhiqiang Wang", "Yichao Gao", "Yanting Wang", "Suyuan Liu", "Haifeng Sun", "Haoran Cheng", "Guanquan Shi", "Haohua Du", "Xiangyang Li"]
  datePublished: "2025-08-19"
  keywords: ["ツールポイズニング", "Model Context Protocol", "LLM エージェント", "ベンチマーク"]
reviewed_by: "joyk0117"
---

この論文の出発点は、[[DefinedTerm/model-context-protocol]]（MCP）が LLM エージェントに外部ツールへの標準化されたインターフェースを与える一方で、信頼できないツールを通じた新たな攻撃対象領域も生み出しているという観察である。先行研究がツールの出力を通じて注入される攻撃に焦点を当てていたのに対し、本論文は著者らがより根本的な脆弱性と呼ぶ[[DefinedTerm/tool-poisoning]]を調査する。これは、ツールが実行されることなく、ツールのメタデータに悪意のある指示が埋め込まれる攻撃である。著者らは、この脅威がこれまで主に個別の事例を通じて示されてきただけで、体系的かつ大規模な評価は行われていなかったと主張する。

このギャップを埋めるため、著者らは [[Dataset/mcptox]] を導入する。彼らはこれを、現実的な MCP 環境においてツールポイズニングに対するエージェントの堅牢性を体系的に評価する初のベンチマークと説明している。MCPTox は、稼働中の実世界の MCP サーバー 45 個と実在するツール 353 個に基づいて構築されており、3 つの攻撃テンプレートから few-shot 学習によって 1312 件の悪意あるテストケースが生成され、10 カテゴリの潜在的リスクを網羅している。20 の主要な LLM エージェント設定を評価した結果、論文はツールポイズニングに対する脆弱性が広く見られると報告している。

## 主なポイント

- 本論文が対象とするのは、ツールの出力を通じて注入される攻撃ではなく、ツールポイズニング（実行を伴わずにツールのメタデータに埋め込まれる悪意ある指示）である。
- MCPTox は、稼働中の実世界の MCP サーバー 45 個と実在するツール 353 個に基づいて構築されている。
- 3 つの攻撃テンプレートから few-shot 学習によって 1312 件の悪意あるテストケースが生成され、10 カテゴリの潜在的リスクを網羅している。
- 20 の LLM エージェント設定全体で脆弱性が広く見られ、o1-mini では攻撃成功率が 72.8% に達したと報告されている。
- 著者らは、攻撃がより強い指示追従能力を悪用するため、能力の高いモデルほどかえって攻撃を受けやすい場合が多いことを見出している。
- 失敗事例の分析から、エージェントがこれらの攻撃を拒否することはまれであることが示されている。最も拒否率が高かった Claude-3.7-Sonnet でも 3% 未満であり、著者らはこれを、正規のツールを使って不正な操作を行う悪意ある行動に対して既存の安全性アラインメントが有効でないことを示すものと捉えている。

## 補足

著者らは、この知見を脅威の理解と緩和のための実証的なベースラインとして提示し、検証可能な形でより安全なエージェントを開発するために MCPTox を公開している。本論文は 2025 年 8 月 19 日に arXiv に投稿され、Cryptography and Security（cs.CR）と Machine Learning（cs.LG）に分類されている。
