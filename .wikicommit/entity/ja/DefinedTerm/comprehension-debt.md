---
title: "理解の負債"
type: "schema:DefinedTerm"
lang: ja
tags: [技術的負債, ソフトウェアエンジニアリング, 認知]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/comprehension-debt.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "開発チームが自らのコードベースについて知っていることと、それを効果的に保守・変更するために実際に理解している必要があることとの間で広がっていくギャップ。生成 AI ツールの導入に伴う社会認知的なリスクとして提唱されている。"
---

理解の負債（Comprehension Debt、CD）とは、開発チームが自らのコードベースについて知っていることと、そのコードベースを効果的に保守・変更するために実際に理解している必要があることとの間で広がっていくギャップである。この用語は [[ScholarlyArticle/comprehension-debt-in-genai-assisted-software-engineering-projects]] で提唱されたもので、同論文はこれを、ソフトウェア開発への生成 AI ツールの導入によってもたらされる社会認知的なリスクとして位置づけている。そうしたツールは認知負荷を減らすが、本来であれば作業を進める過程で築かれていたはずの理解が築かれなくなる。同論文は、この概念が従来の技術的負債とは異なると論じている。負債がコードベースそのものではなく、開発チームの集合的な認知の中に存在するからである。

## 用法

提唱元の研究は、学部生のソフトウェアエンジニアリング・プロジェクトで観察された、理解の負債が蓄積する四つのパターンを挙げている。生成されたコードを理解しないまま受け入れる「ブラックボックスとしての AI」によるコードの受け入れ、コンテキストの不一致による負債、依存が引き起こす能力の萎縮、そして検証の回避である。また、緩和的なパターンも一つ挙げている。同じツールを理解のための足場として使い、開発者がツールとのやり取りを迂回するのではなく、そのやり取りを通じてコードへの理解を深めるというものである。

この負債はチームが書いたものではなくチームが集合的に知っていることの中にあるため、同研究が提案する対応策はコードの変更ではなく実践である。すなわち、検証の実践、構造化された振り返り、そして能動的な学習評価である。

## 関連用語

- [[DefinedTerm/cognitive-debt]]
- [[DefinedTerm/verification-debt]]
- [[DefinedTerm/skill-atrophy]]
- [[DefinedTerm/automation-bias]]
