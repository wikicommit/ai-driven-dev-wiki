---
title: "Crush、おかえり"
type: "schema:BlogPosting"
lang: ja
tags: [コーディングエージェント, ターミナルエージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/BlogPosting/crush-welcome-home.md"
source_commit: "136844949634913857d6d1eb26ef9cb9cfaf8876"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Charm のブログに掲載された 2025 年 7 月の記事。Charm のライブラリ上に構築されたターミナルベースの AI コーディングエージェント Crush が Charm に加わったことを発表し、ターミナルこそが AI 支援開発にふさわしいインターフェースだと論じている。"
  author: ["Christian Rocha"]
  datePublished: "2025-07-30"
  publisher: "[[Organization/charm]]"
---

[[Organization/charm]]のブログに掲載された Christian Rocha によるこの記事は、ターミナルベースの AI コーディングエージェントである[[SoftwareApplication/crush]]が Charm に「帰ってきた」ことを発表している。副題がその位置づけを要約している。「私たちはコマンドラインを魅力的にした。今度はそれを賢くする。」

記事は、Crush の最初の作者である Kujtim Hoxha が Charm スタックの中核の上に Go でこのエージェントを構築したこと、Charm のチームがそれに注目したこと、そしてプロジェクトが現在、最初の作者とともに、Charm チームの全面的な支援を受けて続いていることを語る。記事の残りの部分では、なぜ今この時期が、そしてなぜターミナルが、AI を活用した開発ツールにふさわしいのかを論じている。

## 要点

- Crush は Charm の Bubble Tea、Bubbles、Lip Gloss、Glamour の各ライブラリの上に構築されており、記事によれば Charm はそれらを過去 5 年間にわたって開発し、磨き上げてきた。
- 記事は、LLM が見栄えのするデモの段階を越え、複雑な複数ファイルにまたがる推論を扱える本当に役立つツールになったと論じる。その例として著者は、ウェブサイトの背景エフェクトに使う GLSL シェーダーを Crush で数分のうちに作ったと述べており、そうでなければ数時間かかっていた作業だとしている。
- 強力な AI は方程式の半分にすぎず、それにふさわしいインターフェースはターミナルだと記事は主張する。開発者はすでにそこで作業しており、ターミナルは高速で、スクリプト化でき、既存のワークフローと統合できるからである。
- この説明によれば、Crush は git、docker、npm、ghc、sed、nix など、開発者が使えるのと同じツールを直接使うことができる。
- 記事は、Charm の次世代ターミナル UI ツールキットである Ultraviolet を、同社がターミナルアプリケーションに「さらに力を注ぐ」ものとして紹介している。
- 記事は、GitHub スター 15 万以上、GitHub フォロワー 1 万 1,000 人以上という Charm のコミュニティと、「魅力的なソフトウェアは戦力を何倍にも高める」という主張で締めくくられている。

## 背景

この記事は Charm の創業者が書いた企業の発表であり、ターミナルを AI コーディングツールの本拠地とする議論は同社自身の立場である。Crush が他のコーディングエージェントとどう比較されるのか、また構築の基盤となるライブラリ以外に内部でどのように動作するのかについては、何も述べていない。
