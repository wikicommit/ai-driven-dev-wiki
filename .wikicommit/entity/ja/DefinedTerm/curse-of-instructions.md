---
title: "指示の呪い"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/curse-of-instructions.md"
source_commit: "ecc1bee15ae3ca4148e95adec43c589c16f912f2"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "1 つのプロンプトに積み上げる指示が増えるほど、言語モデルが個々の指示に従う度合いが大きく低下するという知見。多数のルールを一度に提示すると、従われるものと見落とされるものが出てくる。"
---

指示の呪いとは、1 つのプロンプトにまとめる指示が増えるほど、言語モデルが個々の指示に従う能力が低下するという、名前の付いた研究上の知見である。この効果に関する研究では、GPT-4 や Claude でさえ多数の要件を同時に満たすのに苦労することが分かったと報告されている。詳細なルールを 10 個提示されると、モデルは最初のいくつかには従っても、残りを見落とし始めることがある。

## 用法

この知見は、大きな仕様を、すべてを列挙した単一のプロンプトとしてではなく、順を追った単純な指示に分解する理由として引用される。要件一式をまとめて提示するのではなく、モデルを一度に 1 つの部分問題に集中させ、それを完了させてから次に進むのである。

## 関連用語

[[BlogPosting/good-spec]]
