---
title: "指示の呪い"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/curse-of-instructions.md"
source_commit: "09b655594ff0cebcc127385c76c7c935da284a27"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "一つのプロンプトに指示を積み重ねるほど、言語モデルが個々の指示を守る度合いが著しく落ちるという研究上の知見。多くの規則を一度に提示すると、守られるものと見落とされるものが出てくることになる。"
---

指示の呪いとは、一つのプロンプトに指示を多く組み合わせるほど、言語モデルが個々の指示に従う能力が落ちるという、名前の
付いた研究上の知見である。この効果についての研究では、GPT-4 や Claude でさえ多くの要件を同時に満たすのに苦労することが
見出されたと報じられている。詳細な規則を 10 個提示されたモデルは、最初のいくつかには従い、残りを見落とし始めうる。

## 用法

この知見は、大きな仕様を、すべてを一度に列挙する単一のプロンプトではなく、逐次的で単純な指示へ分解する理由として
引かれる。要件一式をまとめて提示するのではなく、モデルを一度に一つの部分問題へ集中させ、それを完了させてから次へ移る、
というやり方である。

## 関連用語

[[BlogPosting/good-spec]]
