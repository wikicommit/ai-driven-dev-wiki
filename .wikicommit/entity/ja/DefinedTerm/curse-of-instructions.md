---
title: "指示の呪い"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/curse-of-instructions.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "1 つのプロンプトに多くの指示を詰め込むほど、言語モデルが個々の指示に従う度合いが大きく低下するという知見。多くのルールを一度に提示すると、従われるものもあれば見落とされるものもある。"
---

指示の呪い（curse of instructions）とは、1 つのプロンプトにより多くの指示が組み合わされるにつれて、言語モデルが個々の指示に従う能力が低下するという、名前のついた研究上の知見である。この効果に関する研究では、GPT-4 や Claude でさえ多くの要件を同時に満たすことに苦戦したと報告されている。10 個の詳細なルールを提示されると、モデルは最初のいくつかには従うものの、残りを見落とし始めることがある。

## 用法

この知見は、大きな仕様を、すべてを一度に列挙した 1 つのプロンプトにするのではなく、順を追った単純な指示に分解する理由として引用される。すなわち、要件一式をまとめて提示するのではなく、モデルを一度に 1 つの部分問題に集中させ、それを完了させてから次に進むということである。

## 関連用語

[[BlogPosting/good-spec]]
