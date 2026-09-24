---
title: "意味の拡散（Semantic Diffusion）"
type: "schema:DefinedTerm"
lang: ja
tags: [用語, ソフトウェアエンジニアリング]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/semantic-diffusion.md"
source_commit: "c6bf44a9d0262400c75a0abf7dee6a8fbb53ff80"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "ある用語が、それを作った人々の外へ広まるにつれてその定義が弱まっていくこと。2006 年に Martin Fowler が作った言葉であり、ここでは vibe coding の受け止められ方に当てはめられている。vibe coding の狭い本来の意味は、すでにより緩い意味に取って代わられつつあると報告されていた。"
---

意味の拡散とは、ある人物や集団がそれなりに良い定義とともに作った言葉が、より広いコミュニティに広まる過程でその定義が弱まっていくときに起こる現象である。この弱まりは定義を完全に失わせ、それとともにその用語が持っていた有用性をも失わせるおそれがある。この用語は 2006 年に Martin Fowler が作ったものであり、彼はその仕組みを本質的には伝言ゲームの連続だと説明した。そこでは、用語を作った人々以外の人々が、本来の定義に従うよう注意を払うことなくその用語について語り始める。これは誰かが意図的に行う実践ではなく、技術用語における失敗モードを名指すものである。

## 用法

この用語は、ある専門用語がなぜ役に立たなくなったのかを診断するために使われる。最初の定義が悪かったのではなく、その定義がより広い読者へと伝わる過程を生き延びられなかった、という診断である。Simon Willison は 2025 年 3 月の文章で、[[DefinedTerm/vibe-coding]] の受け止められ方をこの効果の一例として示している。彼は、この用語が本来意図された意味、すなわち人間が書かれた内容をレビューせずに LLM で書かれたコードという意味に反して、LLM がコードを書くあらゆる場合を指すようにすでに歪められつつあると不満を述べており、その不満を述べる中で Fowler の用語に出会った。彼自身はその苛立ちを、「for a few glorious moments we had the chance at having ONE piece of AI-related terminology with a clear, widely accepted definition」（ほんのわずかな輝かしい間、私たちは明確で広く受け入れられた定義を持つ AI 関連の用語を 1 つだけ持てるチャンスを手にしていた）と表現し、人々が Andrej Karpathy の元の投稿を最後まで読むとは信頼できなかったと述べている。彼は、自身が作った言葉である [[DefinedTerm/prompt-injection]] にも、それまでの 2 年ほどの間に同じことが起きたと報告している。

Willison は、このような意味の希薄化を苛立たしいものの、どうやら避けられないものだと見なしている。そして Fowler の指摘として、これは人気のある用語ほど起こりやすいと述べている。その理由は、用語が人気であるほど伝言ゲームが起こる可能性が高くなり、連鎖が長くなるにつれて誤解が増えていくからである。この効果は、用語を作った本人が単に覆せるものではないようである。vibe coding を作った Karpathy は Willison の記事に対し、定義が落ち着くまでには時間がかかると応じ、自身の実践について、完全に vibe coding に振り切ることはめったになく、たいていはまだコードを見て、複雑さを少しずつ加え、各部分がどう機能するかを学ぼうとしていると述べた。

## 関連用語

- [[DefinedTerm/vibe-coding]] — その希薄化がここで現在の例として示されている用語
- [[DefinedTerm/prompt-injection]] — 同じソースが、同じ効果を被ったと報告しているより以前の造語
