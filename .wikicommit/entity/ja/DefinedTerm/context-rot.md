---
title: "コンテキストロット"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント, コンテキストウィンドウ, LLM]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/context-rot.md"
source_commit: "b0cc6ca63c7e8c23683ba90cc3b5cf0b4690d315"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "コンテキストウィンドウ内のトークン数が増えるにつれて、言語モデルが自らのコンテキストから情報を正確に想起する能力が低下すること。"
---

コンテキストロットとは、コンテキストウィンドウ内のトークン数が増えるにつれて、言語モデルが自らのコンテキストから情報を
正確に想起する能力が低下することである。Anthropic はこの概念を、干し草の中の針（needle-in-a-haystack）型のベンチマークに
ついての諸研究に帰しており、モデルによって劣化の緩やかさに差はあるものの、この特性はあらゆるモデルにわたって現れると
報告している。その実務上の帰結は、コンテキストを満たすべき容器としてではなく、限界効用の逓減する有限の資源として扱わ
ねばならないということである。

## 用法

コンテキストロットは、Anthropic が [[DefinedTerm/context-engineering]] の根拠として挙げる経験的な地盤である。
コンテキストが大きくなるにつれて想起が劣化するため、目標は、関連しうるものを何もかも供給することではなく、信号濃度の
高いトークンのできるかぎり小さい集合を見つけることになる。Anthropic はこの効果を、断崖ではなく性能の勾配として特徴
づけている——モデルは長いコンテキストでも高い能力を保つが、短いコンテキストでの性能と比べると、情報の検索と長距離の
推論において精度の低下を示しうる。

これはまた、コンテキストウィンドウの大きさについての Anthropic の立場も形づくっている。Anthropic は、より大きな
ウィンドウを待つことは魅力的な方策ではあるが、当面この問題を解決しそうにないと論じている。エージェントの最も強い性能が
求められる場面ではどこでも、あらゆる大きさのウィンドウがコンテキストの汚染と情報の関連性の問題にさらされ続けるからで
ある。長い地平の作業に向けて同社が推奨する 3 つの技法——[[DefinedTerm/compaction]]、
[[DefinedTerm/structured-note-taking]]、[[DefinedTerm/sub-agent-architecture]]——は、これらの制約に直接対処する手立てと
して提示されている。

長時間稼働するエージェントについての後の記事は、コンテキストウィンドウの硬いトークン上限と並べてコンテキストロットを、
数時間ないし数日にわたるエージェントの実行がひたすら大きなコンテキストウィンドウに頼るだけでは済まない理由の一つとして
挙げている。劣化はその硬い上限に達するはるか手前から効いてくると述べられている。

## 関連用語

- [[DefinedTerm/attention-budget]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/long-running-agent]]
