---
title: "コンテキストポイズニング"
type: "schema:DefinedTerm"
lang: ja
tags: [コンテキストウィンドウ, LLM, エージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/context-poisoning.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM に生成タスクの前提として与えられる情報に誤りやノイズが混入することで、局所的には整合しているが全体としては誤った出力が生み出されること。"
---

コンテキストポイズニング（context poisoning）とは、生成タスクの前提として言語モデルに与えられる情報に誤りやノイズが混入することで、局所的には論理的に整合しているが全体としては誤った出力をモデルが生み出してしまう現象である。[[BlogPosting/spec-driven-development-context-engineering-custom-slash-commands]] は、これを [[DefinedTerm/context-engineering]]（コンテキストエンジニアリング）が対処すべき三つの問題の一つとして、[[DefinedTerm/context-rot]]（コンテキストロット）および [[DefinedTerm/context-confusion]]（コンテキストの混乱）と並べて挙げている。同記事の説明によれば、その症状は、誤った実装やドキュメント、そして現行の仕様と矛盾する実装や説明である。

## 用法

同記事は、その原因を、古くなった仕様、更新されないままのコメント、タスクと無関係な類似コードなどがコンテキストに紛れ込むことに求めている。モデルは与えられた情報と整合する回答を出そうとするため、入力に含まれる誤りを「きれいな形で」再生産してしまう。

同記事が [[DefinedTerm/custom-slash-commands]]（カスタムスラッシュコマンド）の設計について述べるところでは、コンテキストポイズニングは、すべてのコマンドに結果をファイルへ書き出させる理由の一つとなっている。コンソールにしか残らない出力はそのセッション内でしか使えず、それはコンテキストをリセットできないことに等しい。そして過負荷のコンテキストを持ち越すことは、コンテキストポイズニングとコンテキストロットを招く。あるコマンドから次のコマンドへファイルを受け渡し、その間にコンテキストを消去することが、こうして持ち越されるノイズを断つ方法として示されている。

## 関連用語

- [[DefinedTerm/context-rot]]
- [[DefinedTerm/context-confusion]]
- [[DefinedTerm/context-engineering]]
