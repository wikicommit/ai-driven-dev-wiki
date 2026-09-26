---
title: "PR-Issue アラインメント"
type: "schema:DefinedTerm"
lang: ja
tags: [コードレビュー, トレーサビリティ]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/pr-issue-alignment.md"
source_commit: "afa0bb4898215e961bafe4ec6d65cb547006eeb2"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Isik らによる定式化において、プルリクエストが紐づく Issue の要件を完全かつ正確に実装しているかどうか。Exact、Tangling、Missing、Missing and Tangling の 4 つのカテゴリに分類される。"
---

PR-Issue アラインメントとは、Isik らが定式化し、
[[ScholarlyArticle/rethinking-code-review-in-the-age-of-ai-a-vision-for-agentic-code-review]] で説明されているように、
プルリクエストが、関連する Issue で指定された要件を完全かつ正確に実装しているかどうかである。この定式化は 4 つの
アラインメントのカテゴリを定義している。**Exact** は、プルリクエストが無関係な変更を含まずに要件を完全に満たしている
もの、**Tangling** は Issue と無関係な変更を含むもの、**Missing** は Issue に完全には対応していないもの、そして
**Missing and Tangling** はその両方の逸脱を併せ持つものである。

## 用法

このビジョン論文は、概念とその 4 つのカテゴリの定式化を、同論文が引用するその先行研究に帰しており、PR-Issue
アラインメントの判断をプルリクエストのレビュアーにとっての重大な課題として説明している。同論文はこの概念の起源を、
コミット単位の二値分類に焦点を当てていた tangled commit（もつれたコミット）の研究にさかのぼり、PR-Issue アラインメントを、
その考え方をプルリクエストとその Issue とのより広い関係へと拡張したものとして位置づけている。同論文によれば、Missing の
プルリクエストは技術的負債の兆候である一方、Tangling のプルリクエストは、重要な変更が見落とされかねないノイズを加える
ことでレビューと欠陥の検出を妨げ、また無関係な部分に異論があると、それ以外は正しい変更の承認を遅らせることもある。
同論文は、変更セットの 7〜20% にもつれた変更が含まれ、プルリクエストの 16.5% が Missing とラベル付けされたと報告する
先行研究を引用している。

同論文が提案するレビューのフレームワークでは、アラインメント分析エージェント（Alignment Analysis Agent）がこのチェックを
自動化する。このエージェントは、Issue のタイトル・説明・受け入れ基準を、プルリクエストの詳細とコード差分とともに取得し、
プルリクエストを 4 つのカテゴリのいずれかに分類し、レビューのインターフェース上でもつれた行や無関係な追加を強調表示し、
もつれた変更の行番号と欠けている実装の詳細を報告して、レビュアーが修正を依頼できるようにする。同論文は PR-Issue
アラインメントをキーワードの 1 つに挙げ、PR Augmentation 段階における 4 つの分析の 1 つとして扱っている。

## 関連用語

[[DefinedTerm/lgtm-smell]], [[DefinedTerm/agentic-code-review]], [[DefinedTerm/modern-code-review]]
