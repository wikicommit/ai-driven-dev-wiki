---
title: "AIDev"
type: "schema:Dataset"
lang: ja
tags: [プルリクエスト, 実証研究, エージェンティックコーディング, GitHub]
review_status: pending
translated_from: ".wikicommit/entity/en/Dataset/aidev.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "自律的なコーディングエージェントが関与した GitHub のプルリクエストのデータセット。HuggingFace で配布され、プルリクエスト・レビュー・レビューコメントを扱うリンクされたテーブル群として構造化されている。"
  creator: ""
  datePublished: ""
  measurementTechnique: ""
  sameAs: "https://huggingface.co/datasets/hao-li/AIDev/viewer/pr_review_comments"
---

AIDev は、自律的なコーディングエージェントが関与した GitHub のプルリクエストのデータセットであり、HuggingFace で配布され、エージェンティックなプルリクエストのワークフローに関する研究の実証的基盤として用いられている。[[ScholarlyArticle/code-review-agents-in-pull-requests]] は分析のすべてをこのデータセットから引き出しており、ここでの構造の説明は、データセットの完全な仕様ではなく、その論文が利用したテーブルについての記述である。

## 構成

その研究が中心に据えているテーブルは `PRReviewComment` で、プルリクエストのレビューコメント 19,450 件のレコードを保持している。各コメントは、それを投稿したレビュアーの名前または識別子、そのレビュアーを「User」（人間）か「Bot」（自動化されたエージェント）のいずれかに分類する `user_type` フィールド、コメントの本文、そして親となるプルリクエストを指す `pull_request_url` を持つ。

さらに2つのテーブルが結果のデータを供給する。`PRReview` は COMMENTED、APPROVED、CHANGES_REQUESTED、DISMISSED の値を取るレビューの `state` 属性を提供し、`PullRequest` は PR の open／closed の状態と、その PR が一度もマージされなかった場合には null になる `merged_at` タイムスタンプを提供する。これらのテーブルは `pr_id` と `pull_request_review_id` で結合される。

コメントのレコードをプルリクエスト単位で集約し、レビューコメントが少なくとも1件ある PR のみを残すと、その研究の手元では 3,177 件のユニークな PR が得られ、コードレビューではなく CI/CD やワークフローの自動化を行うボットを除外した後には 3,109 件に減る。

## 評価における利用

このデータセットが支えるのは、能力のベンチマークではなく結果の分析である。レビュアーの識別情報、レビュアーの種別、コメントのテキスト、マージの状態がすべてリンクされているため、レビュアーの構成ごとにマージ率と放棄率を比較したり、レビューコメントの内容をスコアリングしたりするのに使える。上記の研究はまさにそのために用い、エージェントのみがレビューした PR のマージ率 45.20% を、人間のみの 68.37% に対して導出している。

スコープの限界として述べられているのは、対象が AI 生成コードを含むオープンソースの GitHub リポジトリであるため、そこから得られた知見がプロプライエタリなリポジトリ、他のプラットフォーム、あるいはレビューエージェントをまったく使わないプロジェクトへ一般化するとは限らない、という点である。同じ研究は、対象となるリポジトリが多様な領域・規模・成熟度にわたっていることを強みとして注記している。
