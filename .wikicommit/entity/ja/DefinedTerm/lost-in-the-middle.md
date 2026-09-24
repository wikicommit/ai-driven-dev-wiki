---
title: "Lost in the Middle"
type: "schema:DefinedTerm"
lang: ja
tags: [LLM, コンテキストウィンドウ, コンテキストエンジニアリング]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/lost-in-the-middle.md"
source_commit: "07f44d78c36c0f3ef8211927eac4fa818f178ac1"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "言語モデルが、長い入力のまさに冒頭と末尾にあるものには強く反応する一方で、その中ほどに位置する素材をうまく活用できないことを指す名称。"
---

Lost in the Middle とは、言語モデルが長い入力の中ほどに置かれたコンテンツをうまく活用できず、その入力の冒頭と末尾が最も強く反応する位置となる現象に与えられた名称である。[[BlogPosting/making-ai-follow-team-rules]] はこの名称を独自のものとしてではなく、すでに広く流通しているものとして用い、長い入力を与えられたときにモデルが中ほどにあるものを使わない現象だと説明したうえで、同じ状況はコンテキスト汚染（context pollution）とも呼ばれると付言している — ただしこの同一視は主張されるのみで、展開はされていない。

## 使われ方

同記事が引き出す帰結は、量的なものではなく位置的なものである。すなわち、セッションの先頭に置かれた素材は先頭にとどまらない。コーディングエージェントがセッションの進行とともにファイルの読み込み、生成したコード、テスト出力を蓄積していくにつれ、開始時に読み込まれた指示は入力の中ほど — モデルが最も注意を向けない位置 — へと押しやられていく。示されている説明によれば、ループのおよそ 30 回目のイテレーションに達する頃には、エージェントはセッション開始時に読んだルールよりも、直前に読んだコードやコンテキストのほうを信頼するようになり、会話の先頭はもはや先頭とは感じられなくなる。

このように読むと、この用語は指示の品質ではなく *配置* の失敗モードを表しており、同記事では、`AGENTS.md` のようなプロジェクトルートの指示ファイルだけでは不十分である理由としてこの用語が用いられている。ルールは提供されており、誤ってもいなかったが、単にモデルが使わない位置に行き着いてしまったのである。そこで提案されている対策は、よりよく書かれたファイルではなく、エージェントループ内のいくつかの時点で関連するルールを再注入することである — [[SoftwareApplication/pfmls-stylepack]] を参照。

## 関連用語

[[DefinedTerm/context-rot]]、[[DefinedTerm/context-engineering]]、[[DefinedTerm/agents-md]]、
[[DefinedTerm/curse-of-instructions]]
