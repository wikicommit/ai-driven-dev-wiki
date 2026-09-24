---
title: "SE 自律性レベル（SE1.0–SE5.0）"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/se-autonomy-levels.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "ソフトウェアエンジニアリングにおける AI の関与を分類する 6 段階の階層（Level 0–5、SE1.0–SE5.0 に対応）。エージェンシー（与えられた計画を実行すること）と自律性（目標を独自に策定すること）を区別し、自動運転の SAE レベルをモデルにしている。"
---

SE 自律性レベルは、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提案された 6 段階の階層であり、エージェンシー（与えられた目標を達成するために行動し計画を実行するシステムの能力）と、自律性（自らを統治し、そうした目標を独自に策定するシステムの能力）を区別する。この区別の上に、ソフトウェアエンジニアリングにおける AI の関与の 6 つのレベルを対応づけ、米国自動車技術者協会（Society of Automotive Engineers）による自動運転の自動化レベルとの明示的な対比を描いている。

## 用法

6 つのレベルは次のとおりである。**Level 0, Manual Coding（SE1.0）** — AI による対応づけはなく、人間がプレーンなテキストエディタを使ってアイデアを手作業でコードに翻訳する。SAE Level 0（自動化なし）に相当する。**Level 1, Token Assistance（SE1.5）** — 標準的な IDE のオートコンプリートのように、開発者の直近の編集意図を予測トークンに対応づける。SAE Level 1（運転支援）に相当する。**Level 2, Task-Agentic（SE2.0）** — 計画されたコード変更を、生成されたひとまとまりのコードブロックに対応づける（例: GitHub Copilot、Amazon CodeWhisperer）。SAE Level 2（部分的自動化。人間が監督しなければならない）に相当する。**Level 3, Goal-Agentic（SE3.0）** — 技術的な目標（例: 「キャッシュ層を追加する」）を、コード変更の複数ステップの計画に対応づける。Cognition の [[SoftwareApplication/devin]]、Anthropic の [[SoftwareApplication/claude-code]]、Google の [[SoftwareApplication/google-jules]]、OpenAI の Codex といった新興のエージェントがこのレベルを目指しており、SAE Level 3（条件付き自動化）に相当する。**Level 4, Specialized Domain Autonomy（SE4.0）** — 特定ドメインに対する広範な技術的使命（例: 「決済サービスの信頼性を確保する」）を、具体的な技術的目標のリストに対応づける。技術スタックの軸または品質特性の軸に沿って特化し、SAE Level 4（ジオフェンスで区切られたドメイン内での高度自動化）に相当する。**Level 5, General Domain Autonomy（SE5.0）** — 一般的な技術的使命を、未知のあらゆるドメインについてドメイン固有の使命に対応づける。論文はこのレベルがまだ存在せず、概念・研究段階にあると述べており、SAE Level 5（完全自動化）に相当する。

論文は、差し迫った、業界を方向づける課題は Level 3（SE3.0、「Agentic SE」）の習熟にあると述べる。Level 2 から Level 3 への移行は、ワークフローのオーケストレーション、信頼、検証に複雑さをもたらすことで人間とコンピュータの関係を根本的に変えるためである。そしてコミュニティは、完全な自律性（Level 4–5）を現実的に追求する前に、目標エージェント型のシステムのための規律ある実践を確立しなければならないとしている。

## 関連用語

[[DefinedTerm/structured-agentic-software-engineering]], [[DefinedTerm/agentic-autonomy-levels]]（別の著者が提案した、AI コーディングエージェントのための 2 軸からなる別個の自律性スキーム）
