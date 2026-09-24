---
title: "指示の呪い"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/curse-of-instructions.md"
source_commit: "0426e7f2036ea739db9b2cbdbaaed396066f6d6c"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "単一のプロンプトに積み上げる指示が増えるほど、言語モデルが個々の指示を守る度合いが大きく低下するという知見。多数のルールを一度に提示すると、守られるものと見落とされるものが出てくる。"
---

指示の呪い（curse of instructions）とは、単一のプロンプトに組み合わせる指示が増えるほど、言語モデルが個々の指示に従う能力が低下するという、名前の付いた研究上の知見である。この効果に関する研究では、GPT-4 や Claude でさえ多くの要求を同時に満たすのに苦労することが分かったと報告されている。10 個の詳細なルールを提示されると、モデルは最初のいくつかには従っても、残りを見落とし始めることがある。

## 用法

この知見は、大きな仕様をすべてを一度に列挙した単一のプロンプトにするのではなく、逐次的で単純な指示へと分解する理由として引かれる。すなわち、要求の全体を一度に提示するのではなく、モデルを一度に 1 つの部分問題に集中させ、それを完了させてから次へ進むのである。

## 関連用語

[[BlogPosting/good-spec]]
