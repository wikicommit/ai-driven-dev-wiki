---
title: "Edit apply モデル"
type: "schema:DefinedTerm"
lang: ja
tags: [コーディングエージェント, コード編集]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/edit-apply-model.md"
source_commit: "d5488c1df4d0cbce781137bbb410c0d112fd8758"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "大きなモデルが望む変更を Markdown の説明として書き、小さなモデルがその説明からファイル全体を書き直す、コード編集の設計。大きなモデルが正しく整形された diff を確実に出力できなかった 2024 年に、コーディングエージェント、IDE、アプリビルダーの間で一般的だった。"
---

Edit apply モデルとは、2 つのモデルからなるコード編集の構成で用いられる小さなモデルである。大きなモデルが何を変更するかを
決めて編集内容を Markdown の説明として記述し、続いて小さな "edit apply" モデルが、その説明を実行するようにファイル全体を
書き直す。[[BlogPosting/dont-build-multi-agents]] が述べるところでは、この発想は、当時は大きなモデルに正しく整形された
diff を出力させるよりも、小さなモデルに説明からファイル全体を書き直させるほうが確実だった、という観察に基づいていた。

## 用法

同投稿は、このパターンを、多くのモデルがコードの編集を苦手としていた 2024 年に、[[SoftwareApplication/devin]] を含む
コーディングエージェント、IDE、アプリビルダーの間で一般的だった実践として説明している。同投稿はこのパターンを、判断と
行動が複数のモデルに分割されたときに何がうまくいかなくなるかの例として用いる。小さなモデルは大きなモデルの指示を
しばしば誤解し、指示にほんのわずかな曖昧さがあるだけで誤った編集を行ってしまっていた。同投稿は、現在では編集の
意思決定と適用は、単一のモデルによって一つのアクションで行われることが多くなっていると付け加えている。

## 関連用語

- [[DefinedTerm/context-engineering]] — 同投稿は、判断の衝突を避けるようにエージェントを設計することの実例の一つとして、
  このパターンを取り上げている
