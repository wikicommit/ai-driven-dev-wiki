---
title: "大規模言語モデルのための Agent Skills：アーキテクチャ、獲得、セキュリティ、そして今後の道筋"
type: "schema:ScholarlyArticle"
lang: ja
tags: [エージェントスキル, エージェントアーキテクチャ, サーベイ, エージェントセキュリティ]
review_status: pending
translated_from: ".wikicommit/entity/en/ScholarlyArticle/agent-skills-for-large-language-models.md"
source_commit: "e3a247123c2e2c5a1d19244743218b709c140afd"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Agent Skills ── エージェントが必要に応じて読み込む、指示・コード・リソースからなる組み合わせ可能なパッケージ ── の全体像を、4 つの軸（アーキテクチャ、獲得、大規模なデプロイ、セキュリティ）に沿って整理したサーベイ。あわせて Skill Trust and Lifecycle Governance Framework を提案している。"
  author: ["Renjun Xu", "Yang Yan"]
  datePublished: "2026-02-12"
  keywords: ["Agent Skills", "段階的開示", "Model Context Protocol", "スキル獲得", "エージェントセキュリティ"]
---

本サーベイは、モノリシックな言語モデルからモジュール化されたスキルを備えるエージェントへの移行を、大規模言語モデルが実際にデプロイされる方法における決定的な転換として描いている。すべての手続き的知識をモデルの重みに符号化するのではなく、[[DefinedTerm/agent-skills]] ── 著者らはこれを、エージェントが必要に応じて読み込む、指示・コード・リソースからなる組み合わせ可能なパッケージと説明している ── によって、再学習なしに能力を動的に拡張できる。本サーベイは、これが [[DefinedTerm/progressive-disclosure]]（段階的開示）、ポータブルなスキル定義、[[DefinedTerm/model-context-protocol]] との統合というパラダイムとして形式化されていると述べている。

著者らはこの分野を 4 つの軸で整理している。アーキテクチャ上の基盤、スキルの獲得、大規模なデプロイ、そしてセキュリティである。セキュリティについては、コミュニティが提供したスキルの 26.1% に脆弱性が含まれると報告する最近の実証分析を挙げ、それを根拠に Skill Trust and Lifecycle Governance Framework を提案している。これは、スキルの出自（プロベナンス）を段階的なデプロイ能力に対応づける、4 層のゲートベースのパーミッションモデルである。本サーベイは、LLM エージェントやツール利用を広く扱う先行サーベイとは異なり、新たに現れつつあるスキルという抽象化レイヤーと、それが次世代のエージェント型システムにもたらす意味に特に焦点を当てている点で自らを差別化している。

## 主なポイント

- アーキテクチャ上の基盤の軸では、SKILL.md の仕様、段階的なコンテキストの読み込み、そしてスキルと MCP の相補的な役割を検討している。
- スキル獲得の軸では、スキルライブラリを用いた強化学習、自律的なスキル発見（SEAgent）、組み合わせによるスキル合成を扱っている。
- 大規模なデプロイの軸では、コンピュータ操作エージェント（CUA）のスタック、GUI グラウンディングの進歩、OSWorld と SWE-bench におけるベンチマークの進展を扱っている。
- セキュリティの軸は、最近の実証分析 ── サーベイ自身の測定ではなく、サーベイが引用している研究 ── に基づき、コミュニティが提供したスキルの 26.1% に脆弱性が含まれると報告している。
- 著者らは Skill Trust and Lifecycle Governance Framework を提案している。これは、スキルの出自を段階的なデプロイ能力に対応づける、4 層のゲートベースのパーミッションモデルである。
- 本サーベイは、クロスプラットフォームでのスキルのポータビリティから能力ベースのパーミッションモデルまで、7 つの未解決の課題を挙げ、信頼でき自己改善するスキルエコシステムに向けた研究アジェンダを提案している。

## 補足

本論文は 2026 年 2 月 12 日に arXiv へ初めて投稿され、2026 年 6 月 2 日に最終改訂された（バージョン 4）。ACM Conference on AI and Agentic Systems 2026 の Agent Skills '26 Workshop に採択されており、Multiagent Systems（cs.MA）と Artificial Intelligence（cs.AI）に分類されている。著者らは、自らが概観する分野がそれまでの数か月で急速に進化してきたと述べている。
