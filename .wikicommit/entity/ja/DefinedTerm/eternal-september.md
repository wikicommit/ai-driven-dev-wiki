---
title: "終わらない九月"
type: "schema:DefinedTerm"
lang: ja
aliases: ["Eternal September of open source", "the September that never ended"]
tags: [オープンソース, AI 生成の貢献, メンテナー]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/eternal-september.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "コミュニティの規範に不慣れな新参者が絶え間なく流入し続けることを指す Usenet 時代の用語。GitHub は 2026 年に、作るのは安価だがレビューするのは安価ではない、AI 生成の貢献がオープンソースに押し寄せている状況にこれを当てはめた。"
---

終わらない九月（Eternal September）とは、もともとは Usenet の歴史上のある時期を指す言葉である。毎年九月になると、
その規範に不慣れな大学の新入生の波がオンラインにやってきて、辛抱強く受け入れられていたが、やがて大手のダイヤルアップ
ISP によって新規ユーザーが途切れなく流入するようになり、それは「終わることのなかった九月」となった。2026 年 2 月の投稿
（[[BlogPosting/welcome-to-the-eternal-september-of-open-source]]）で、GitHub はこの用語をオープンソースに当てはめ、
オープンソースはいま独自の終わらない九月を経験していると論じる。その原動力は新規ユーザーだけではなく貢献の量そのもので
あり、生成 AI によって人々がコード、Issue、セキュリティレポートを大量に生み出せるようになった一方で、それらを
レビューするコストは変わらないままだという。

## 用法

GitHub の用法では、この用語は品質の問題だけでなく、信頼の問題を捉えるものである。オープンなコラボレーションは信頼の上に
成り立っており、その信頼はかつて貢献に伴う摩擦によって守られていた。同投稿は、ほとんどの貢献者は善意で行動していると
しつつも、量がレビュー能力を上回る速さで増えると、善意による投稿でさえメンテナーを圧倒しうるものとなり、信頼が揺らぎ
始めると論じる。GitHub はこれを、古くからの問題——ノイズの多い受信、バグ報告のトリアージ、自動スキャナーのレポート——が
新たな規模で続いているものとして扱っている。

同投稿はこのメタファーを楽観的にも用いている。オープンソースの終わらない九月を、参加したいと望む人がかつてないほど多い
ことの表れと呼び、初期のインターネットがコミュニティを大規模に維持するための規範とツールを発展させたように、
オープンソースに必要なのは跳ね橋を上げることではなく、メンテナーのためのより良いシグナルとツールだと論じる。同投稿が
挙げる対応は、誰がプルリクエストを開けるかについてのプラットフォームの制御から、[[SoftwareApplication/vouch]] の
ようなコミュニティの信頼システムや、明文化された [[DefinedTerm/ai-contribution-policy]] のルールにまで及ぶ。

## 関連用語

- [[DefinedTerm/ai-contribution-policy]]
- [[DefinedTerm/review-bottleneck]]
