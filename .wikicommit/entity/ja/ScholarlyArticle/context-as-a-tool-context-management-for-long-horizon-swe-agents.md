---
title: "ツールとしてのコンテキスト：長期タスクに取り組む SWE エージェントのためのコンテキスト管理"
type: "schema:ScholarlyArticle"
lang: ja
tags: [コンテキスト管理, コーディングエージェント, 長期タスク]
translated_from: ".wikicommit/entity/en/ScholarlyArticle/context-as-a-tool-context-management-for-long-horizon-swe-agents.md"
source_commit: "48d80cbbb1b1176580f1d3e42bed65bbe89633ce"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "長期タスクに取り組むソフトウェアエンジニアリングエージェントのために、コンテキストの維持を呼び出し可能なツールとするコンテキスト管理パラダイム CAT を提案する 2025 年の arXiv 論文。あわせて、コンテキストを意識したモデル SWE-Compressor の学習に用いる軌跡レベルの教師づけフレームワークも提案している。"
  author: ["Shukai Liu", "Jian Yang", "Bo Jiang", "Yizhi Li", "Jinyang Guo", "Xianglong Liu", "Bryan Dai"]
  datePublished: "2025-12-26"
  keywords: ["コンテキスト管理", "SWE エージェント", "長期的推論", "コンテキスト圧縮"]
---

この論文は、リポジトリ規模のコードベースとの長期にわたるやり取りを必要とする、現実のソフトウェア
エンジニアリングタスクに取り組む大規模言語モデルベースのエージェントを扱う。論文は、既存のエージェント
の多くが追記のみのコンテキスト維持や受動的にトリガーされる圧縮ヒューリスティクスに頼っており、それが
長時間のやり取りにおいてしばしばコンテキストの爆発、意味のドリフト、推論の劣化につながっていると
論じる。

これに対して論文は、コンテキストの維持をエージェントの意思決定に統合された呼び出し可能なツールへと
格上げするコンテキスト管理パラダイム、[[DefinedTerm/context-as-a-tool]]（CAT）を提案する。ソフト
ウェアエンジニアリングエージェントのコンテキスト管理を支えるため、著者らは軌跡レベルの教師づけ
フレームワーク CAT-GENERATOR も提案し、それを用いてコンテキストを意識したモデル SWE-Compressor を
学習させ、[[Dataset/swe-bench-verified]] で評価している。

## 要点

- CAT は、安定したタスクの意味、凝縮された長期記憶、高忠実度の短期的なやり取りからなる構造化された
  コンテキストワークスペースを形式化する。
- CAT のもとでは、エージェントは受動的にトリガーされる圧縮に頼るのではなく、適切なマイルストーンで
  過去の軌跡を行動に移せる要約へと能動的に圧縮する。
- CAT-GENERATOR は、完全なやり取りの軌跡にコンテキスト管理のアクションを注入するオフラインのデータ
  構築パイプラインに基づいている。
- SWE-Bench-Verified において SWE-Compressor は 57.6% の解決率に達し、著者らによれば、限られた
  コンテキスト予算のもとで安定した長期的推論を維持しつつ、ReAct ベースのエージェントや静的な圧縮の
  ベースラインを大きく上回っている。

## 補足

この論文は 2025 年 12 月 26 日に arXiv に投稿され、Computation and Language（cs.CL）に分類されて
いる。
