---
title: "理解の負債"
type: "schema:DefinedTerm"
lang: ja
tags: [技術的負債, ソフトウェアエンジニアリング, 認知]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/comprehension-debt.md"
source_commit: "59f94553fa52912f703987f31c807ff6a3208a7d"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "開発チームが自らのコードベースについて知っていることと、それを効果的に保守・変更するために実際に理解している必要があることとの間で広がっていく隔たり。生成 AI ツールの導入がもたらす社会的・認知的リスクとして提起されている。"
---

理解の負債（Comprehension Debt、CD）とは、開発チームが自らのコードベースについて知っていることと、そのコードベースを
効果的に保守・変更するために実際に理解している必要があることとの間で広がっていく隔たりである。この用語は
[[ScholarlyArticle/comprehension-debt-in-genai-assisted-software-engineering-projects]] で提起されており、同論文はこれを、
ソフトウェア開発における生成 AI ツールの導入が持ち込む社会的・認知的リスクとして位置づけている。そうしたツールは認知負荷を
減らすが、その作業を行う過程で本来なら築かれたはずの理解は築かれない。同論文は、この概念が従来の技術的負債とは異なると
論じる。それはコードベースそのものではなく、開発チームの集団的な認知のうちに宿るからである。

## 用法

提起元の研究は、学部のソフトウェアエンジニアリングのプロジェクトで観察された、理解の負債が蓄積する 4 つのパターンを
記述している。生成されたコードを理解しないまま受け入れる AI ブラックボックス型のコード受容、コンテキスト不整合による
負債、依存がもたらす萎縮、そして検証の迂回である。同研究はまた、緩和的なパターンを一つ挙げている。同じツールを理解の
足場として用い、開発者がそのやり取りを迂回するのではなくそれを通じてコードへのより深い理解を築いていくというもので
ある。

この負債はチームが書いたものではなくチームが集団として知っていることのうちに宿るため、同研究が提案する対処はコードの
変更ではなく実践である。すなわち、検証の実践、構造化された振り返り、そして能動的な学習の評価である。

## 関連用語

- [[DefinedTerm/cognitive-debt]]
- [[DefinedTerm/verification-debt]]
- [[DefinedTerm/skill-atrophy]]
- [[DefinedTerm/automation-bias]]
