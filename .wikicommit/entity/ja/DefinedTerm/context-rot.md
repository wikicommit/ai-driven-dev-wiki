---
title: "コンテキストロット"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント, コンテキストウィンドウ, LLM]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/context-rot.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "コンテキストウィンドウ内のトークン数が増えるにつれて、言語モデルがそのコンテキストから情報を正確に想起する能力が低下すること。"
---

コンテキストロット（context rot）とは、コンテキストウィンドウ内のトークン数が増えるにつれて、言語モデルがそのコンテキストから情報を正確に想起する能力が低下することである。Anthropic はこの概念を、needle-in-a-haystack（干し草の山から針を探す）型のベンチマークに関する研究に由来するものとし、劣化が他より緩やかなモデルもあるものの、この特性はすべてのモデルに現れると報告している。その実務上の帰結は、コンテキストを、満たすべき容器としてではなく、限界収益が逓減する有限の資源として扱わなければならないということである。

## 用法

コンテキストロットは、Anthropic が [[DefinedTerm/context-engineering]] の経験的な根拠として示すものである。コンテキストが大きくなるにつれて想起が劣化するため、目指すべきは、関係しうるかもしれないものをすべて与えることではなく、高シグナルなトークンの可能な限り小さな集合を見つけることになる。Anthropic はこの効果を、急な崖ではなく性能の勾配として特徴づけている——モデルは長いコンテキストでも高い能力を保つが、短いコンテキストでの性能と比べると、情報検索や長距離の推論の精度が下がることがある。

これはまた、コンテキストウィンドウのサイズについての Anthropic の立場も形づくっている。Anthropic は、より大きなウィンドウを待つことは魅力的な戦術ではあるものの、当面は問題を解決しそうにないと論じる。最高のエージェント性能が求められる場面ではどこでも、あらゆるサイズのウィンドウが依然としてコンテキスト汚染と情報の関連性の問題を抱えるからである。同社が長期にわたる作業のために推奨する三つの技法——[[DefinedTerm/compaction]]、[[DefinedTerm/structured-note-taking]]、[[DefinedTerm/sub-agent-architecture]]——は、これらの制約に直接対処する方法として提示されている。

長時間稼働するエージェントについての後の記事は、コンテキストウィンドウの厳しいトークン上限と並んで、コンテキストロットを、数時間から数日に及ぶエージェントの実行が、ひたすら大きくなるコンテキストウィンドウに単純に頼ることのできない理由の一つとして挙げている。その劣化は、厳しい上限に達するよりずっと前に始まるとされる。

LangChain の [[BlogPosting/the-anatomy-of-an-agent-harness]] は、Chroma による研究にリンクしつつ、コンテキストウィンドウが埋まっていくにつれてモデルが推論やタスクの完了を苦手とするようになることを指してこの用語を使い、それをエージェントハーネスが管理しなければならない問題として扱っている——今日のハーネスを、主として良いコンテキストエンジニアリングを届けるための仕組みだと述べている。同記事は三つのハーネス戦略を挙げる。ウィンドウがほぼいっぱいになったときにコンテキストを要約して退避させる [[DefinedTerm/compaction]]、大きなツール出力の先頭と末尾だけをコンテキストに残し、残りをファイルシステムに書き出す [[DefinedTerm/tool-call-offloading]]、そして [[DefinedTerm/progressive-disclosure]] を用いて、多すぎるツールや MCP サーバーが開始時にコンテキストへ読み込まれないようにする Skills である。そうしたものが読み込まれると、エージェントが作業を始める前から性能が劣化してしまうからである。

## 関連用語

- [[DefinedTerm/attention-budget]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/long-running-agent]]
- [[DefinedTerm/tool-call-offloading]]
- [[DefinedTerm/agent-harness]]
