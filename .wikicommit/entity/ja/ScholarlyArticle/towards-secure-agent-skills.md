---
title: "セキュアな Agent Skills に向けて：アーキテクチャ、脅威分類、セキュリティ分析"
type: "schema:ScholarlyArticle"
lang: ja
tags: [エージェントスキル, エージェントセキュリティ, 脅威モデリング]
review_status: pending
translated_from: ".wikicommit/entity/en/ScholarlyArticle/towards-secure-agent-skills.md"
source_commit: "e3a247123c2e2c5a1d19244743218b709c140afd"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Agent Skills フレームワークのセキュリティ分析。スキルのライフサイクルを 4 つのフェーズで定義し、7 カテゴリ・17 シナリオからなる脅威分類を構築したうえで、確認済みの 5 件のセキュリティインシデントに照らして検証している。"
  author: ["Zhiyuan Li", "Jingzheng Wu", "Xiang Ling", "Xing Cui", "Tianyue Luo"]
  datePublished: "2026-04-03"
  keywords: ["Agent Skills", "脅威分類", "セキュリティ分析", "LLM エージェント"]
---

この論文は [[DefinedTerm/agent-skills]] を、LLM ベースのエージェントがドメイン固有の専門知識を必要に応じて獲得するための、モジュール式でファイルシステムベースのパッケージ形式を定める新興のオープン標準として説明している。複数のエージェント型プラットフォームで急速に採用され、大規模なコミュニティマーケットプレイスも登場しているにもかかわらず、Agent Skills のセキュリティ特性はこれまで体系的に研究されてこなかったと指摘し、本論文をこのフレームワークに対する初の包括的なセキュリティ分析として位置づけている。

著者らは Agent Skill のライフサイクル全体を、作成（Creation）、配布（Distribution）、デプロイ（Deployment）、実行（Execution）の 4 つのフェーズで定義し、各フェーズがもたらす構造的な攻撃対象領域を特定している。それを基に脅威分類を構築し、Agent Skills エコシステムで確認された 5 件のセキュリティインシデントに照らして検証したうえで、脅威カテゴリごとの防御の方向性、未解決の研究課題、ステークホルダーへの提言を論じている。

## 要点

- 論文は Agent Skill のライフサイクルを、作成、配布、デプロイ、実行の 4 つのフェーズとしてモデル化しており、各フェーズにはそれぞれ固有の構造的な攻撃対象領域がある。
- 脅威分類は、3 つの攻撃レイヤーにわたって整理された 7 カテゴリ・17 シナリオで構成され、アーキテクチャ分析と実世界のエビデンスの両方に基づいている。
- この分類は、Agent Skills エコシステムで確認された 5 件のセキュリティインシデントの分析を通じて検証されている。
- 著者らは、最も深刻な脅威はフレームワーク自体の構造的な特性から生じると結論づけている。具体的には、データと命令の境界がないこと、一度の承認で信頼が持続する信頼モデル、そしてマーケットプレイスにおける必須のセキュリティレビューがないことである。
- 著者らは、こうした構造的な脅威は漸進的な緩和策だけでは対処できないと主張している。

## 補足

この論文は 2026 年 4 月 3 日に arXiv に投稿され、Cryptography and Security（cs.CR）と Artificial Intelligence（cs.AI）に分類されている。
