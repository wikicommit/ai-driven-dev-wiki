---
title: "コンテキストの混乱"
type: "schema:DefinedTerm"
lang: ja
tags: [コンテキストウィンドウ, LLM, エージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/context-confusion.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "過剰な情報、抽象的すぎる指示、あるいは互いに矛盾する指示によって、LLM がどの情報を優先すべきか判断できなくなり、出力が不安定になる状態。"
---

コンテキストの混乱（context confusion）とは、過剰な情報、抽象的すぎる指示、あるいは互いに矛盾する指示によって、言語モデルがどの情報を優先すべきか判断できなくなる状態である。[[BlogPosting/spec-driven-development-context-engineering-custom-slash-commands]] は、これを [[DefinedTerm/context-engineering]]（コンテキストエンジニアリング）が対処すべき三つの問題の一つとして、[[DefinedTerm/context-rot]]（コンテキストロット）および [[DefinedTerm/context-poisoning]]（コンテキストポイズニング）と並べて挙げている。同記事の説明によれば、その症状は、実行ごとに結果が大きくばらつくことと、ハルシネーションを起こしやすくなることである。

## 用法

同記事は、その原因をコンテキストの [[DefinedTerm/signal-to-noise-ratio]]（シグナル対ノイズ比）の観点から説明している。タスクが実際に必要とする情報（シグナル）が、無関係な情報や冗長なログ（ノイズ）に比べて占める割合が小さくなると、モデルのアテンションによる重み付けがうまく機能しなくなり、重要な情報が軽く、重要でない情報が重く扱われて、出力の品質が不安定になる。

同記事の具体例は、[[DefinedTerm/custom-slash-commands]]（カスタムスラッシュコマンド）の設計から来ている。Web 調査、ドキュメント作成、ガイドラインチェック、修正を一続きに連結した単一のコマンドが、Web 検索に由来する大量のノイズによって本来の方向から逸らされ、著者はこれがコンテキストの混乱とコンテキストロットを引き起こしたと見ている。同記事が提案する対策は、こうした作業をそれぞれ単一の責務を持つコマンドに分割し、タスクに必要な最小限の情報だけを注入することである。

## 関連用語

- [[DefinedTerm/context-rot]]
- [[DefinedTerm/context-poisoning]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/signal-to-noise-ratio]]
