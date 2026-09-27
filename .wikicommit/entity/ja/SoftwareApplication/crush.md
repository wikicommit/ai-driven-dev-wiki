---
title: "Crush"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングエージェント, ターミナルエージェント]
translated_from: ".wikicommit/entity/en/SoftwareApplication/crush.md"
source_commit: "74c6840463d960cf5b82c76818ec6b07f5f7233d"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Charm のターミナル UI ライブラリを基盤に Go で書かれた、ターミナルベースの AI コーディングエージェント。当初は Kujtim Hoxha によって作られ、現在は Charm で開発されている。"
  applicationCategory: "AI コーディングエージェント"
  author: "[[Organization/charm]]"
---

Crush はターミナルベースの AI コーディングエージェントである。作者は Kujtim Hoxha で、[[Organization/charm]] によれば、彼は 2025 年 7 月の数か月前に、人々の注目を集めるものを作ろうと取り組み始めた。Crush は Charm のスタックの中核である Bubble Tea、Bubbles、Lip Gloss、Glamour の各ライブラリを基盤に Go で書かれている。Charm は [[BlogPosting/crush-welcome-home]] で、このプロジェクトが同社に「帰ってきた」ことを発表した。プロジェクトは同社のもとで、元の作者とともに Charm チームの全面的な支援を受けて継続している。

## 機能

Charm は Crush について、開発者が使えるのと同じコマンドラインツール（git、docker、npm、ghc、sed、nix など）に直接アクセスでき、それらのツールに関する豊富な知識をもって使いこなせると説明している。Crush にできることの一例として、Charm の創業者は、同社ウェブサイトの背景用に多層のガウシアンノイズを生成する GLSL シェーダーを、Crush を使って数分で作ったと述べている。

このツールについてのユーザーによる記述である [[BlogPosting/testing-out-crush-tui-coding-agent]] は、外部から見た Crush を次のような TUI コーディングエージェントとして説明している。編集を行う前に確認を求めるためユーザーは変更ごとに許可または拒否でき、変更したファイルの一覧を保持し、使用中のモデルとそれに伴うコストを表示する。`ctrl-p` のオプションには、モデル間の素早い切り替えやセッションの要約が含まれる。この記事の著者は neovim 内のサイドペインで Crush を実行し、そこでいくつかの表示上のバグがあったと報告している。

## 採用とエコシステム

Charm が Crush を推す論拠は、AI 支援開発のインターフェースとしてのターミナルを推す論拠でもある。開発者はすでにターミナルを日常的に使っており、ターミナルは高速でスクリプト化でき、既存のワークフローと統合できる、というものである。Charm が「現在は Crush と呼ばれている」と述べるこのプロジェクトは、元の作者が Charm チームとともに継続している。

同じユーザーによる記述では、TUI を別にすれば、Crush のモデル非依存な設計（使用するモデルをユーザーが選べること）を最も重要な特徴として扱い、Crush を使って個人サイトの小さな機能を作ったことを報告している。その際は主に Sonnet 4 を使い、ちょっとした編集には Gemini Flash を使ったという。著者は、自分にとってはこうした使い方の API コストが通常のコーディングにおける体験の良さを上回ると結論づけ、高価なモデルを必要としない小さなタスクには引き続き Crush を使うつもりだとしている。
