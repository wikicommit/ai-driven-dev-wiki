---
title: "Nicholas Carlini"
type: "schema:Person"
lang: ja
tags: [研究者, エージェントハーネス, セキュリティ]
review_status: pending
translated_from: ".wikicommit/entity/en/Person/nicholas-carlini.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Anthropic の Safeguards チームの研究者であり、言語モデルに何が達成できるのかの限界をストレステストしている。以前はペネトレーションテストに従事していた。"
  affiliation: "[[Organization/anthropic]]"
  jobTitle: "Researcher"
  birthDate: ""
---

Nicholas Carlini は [[Organization/anthropic]] の Safeguards チームの研究者である。彼が掲げる方法は、言語モデルを限界まで押し進め、それがどこで崩れ始めるのかを研究することであり、そうすることこそがモデルに何ができるのかを理解する最善の道だという理屈による。

## 経歴

ここで利用できる出典は、彼が以前ペネトレーションテストに従事し、大企業の製品の脆弱性を突く仕事をしていたことを記録している。これは、自律的なソフトウェア開発が自分を落ち着かない気持ちにさせる理由を説明する際に彼が持ち出す背景である。それによって、プログラマが自分自身では一度も検証していないソフトウェアをデプロイするという見通しが、抽象的ではなく具体的な懸念になるからだ。

## 業績

彼は [[BlogPosting/building-a-c-compiler-with-parallel-claudes]] で述べられている並列エージェントチームの実験を構築し、報告した。そこでは16のエージェントが、Linux 6.9 をビルドできる10万行の Rust 製 C コンパイラを生み出した。彼は、この C コンパイラのプロジェクトを Claude 4 モデルシリーズを通じた繰り返しの能力ベンチマークとして用いていると述べており、毎回同じ仕様——依存関係を持たないスクラッチからの最適化コンパイラ、GCC 互換、Linux カーネルをコンパイルでき、複数のバックエンドをサポートするよう設計されたもの——を書き起こしつつ、実装のアプローチは意図的に指定しないままにしている。
