---
title: "2 つの出版社と 3 人の著者が「バイブコーディング」の意味を理解していない"
type: "schema:BlogPosting"
lang: ja
tags: [バイブコーディング, 用語, AI 支援プログラミング]
review_status: pending
translated_from: ".wikicommit/entity/en/BlogPosting/two-publishers-and-three-authors-fail-to-understand-what-vibe-coding-means.md"
source_commit: "8747b8ec3dcc7491d2de6b080020106d3f5da014"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Simon Willison は、タイトルに「バイブコーディング」を使った刊行予定の 2 冊の本が、この用語を専門的な AI 支援型エンジニアリングの意味で誤用していると論じる。この用語はもともと、生成されるコードを気にかけずに AI でコードを生成することを意味するために作られたものである。"
  author: ["Simon Willison"]
  datePublished: "2025-05-01"
---

2025 年 5 月 1 日のこの投稿で、Simon Willison は [[DefinedTerm/vibe-coding]] の定義を改めて述べている。それは「コードを書く手助けに AI ツールを使うこと」ではなく、「生成されるコードを気にかけずに AI でコードを生成すること」を意味する。彼は以前の投稿 [[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] を引き合いに出し、この区別を「死守する覚悟のある一線」と呼んでいる。

きっかけは、この用語をまさにそれでないものを指して使っていると彼が言う、刊行予定の 2 冊の本である。Gene Kim と Steve Yegge による [[Book/vibe-coding-building-production-grade-software]]（IT Revolution）と、当時「Vibe Coding: The Future of Programming」というタイトルだった Addy Osmani の O'Reilly の本であり、後者も同様に、専門的なエンジニアが AI 支援型コーディングツールを自分のワークフローにどう組み込めるかを扱っている。2025 年 9 月 4 日に追記された更新では、Osmani の本のタイトルが [[Book/beyond-vibe-coding]] に変わったことが記されており、Willison はこれをずっと良いタイトルだと評している。

## 要点

- Willison は、この用語が Andrej Karpathy によって作られたのは投稿のわずか 84 日前だと述べ、Karpathy のツイートを全文引用して、「コードが存在することさえ忘れる（forget that the code even exists）」と「使い捨ての週末プロジェクトなら悪くない（It's not too bad for throwaway weekend projects）」という言い回しを強調している。
- 彼はこのツイートを、バイブコーディングとはコードの存在を忘れながら使い捨てのプロジェクトを作る楽しいやり方だと定義するものとして読んでいる。それは、本番コードを責任を持って構築するプロセスの一部として LLM ツールを使うこととは同じではない。
- 彼は、用語が作られてからそれを誤って使った最初の本が出版されるまでの期間として、これは記録ではないかと首をかしげ、それらの本の表紙デザインがすでに出来上がっていたことにも触れている。
- 彼が主に残念に思っているのは、本当のバイブコーディングについての本が依然として必要とされていることである。それは、ソフトウェア開発者ではなく、開発者になりたいとも思っていない人々が、自分自身の問題を解決するためにバイブコーディングを安全に、効果的に、責任を持って使えるよう手助けする本である。彼は、バイブコーディングはそうした人々のためのものであり、すでにソフトウェアエンジニアである人々のためのものではないと論じる。
- 彼はそうした本が答えられるであろう未解決の問いを挙げている。どのような種類のプロジェクトがこの方法で作れるのか、セキュリティ、プライバシー、信頼性、使いすぎ（過剰な出費）にまつわる落とし穴をどう避けるのか、そして達成できることとできないことの間にある「ギザギザの境界（jagged frontier）」をどう見極めるのか、である。
- 彼は、おそらくこの議論には負けたのだろうと認め、[[DefinedTerm/semantic-diffusion]] を「止めようのない力」と呼んでいる。

## 背景

この投稿は、「バイブコーディング」を狭い本来の意味に結びつけておこうとする Willison の継続的な取り組みの中の意見記事である。2 冊の本についての主張は、執筆時点で発表されていたタイトル、サブタイトル、説明に基づいており、出版された内容に基づくものではない。
