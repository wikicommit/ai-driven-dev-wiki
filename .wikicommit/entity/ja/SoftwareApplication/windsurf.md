---
title: "Windsurf"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール]
translated_from: ".wikicommit/entity/en/SoftwareApplication/windsurf.md"
source_commit: "74c6840463d960cf5b82c76818ec6b07f5f7233d"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Codeium による AI IDE で、ルールファイルは `.windsurf/rules/` 以下に置かれる。AI IDE ルールに関する 2026 年のマイニングおよびサーベイ研究で調査された 5 つのツールの 1 つ。"
  applicationCategory: "AI IDE"
  author: "Codeium"
---

Windsurf は、Codeium が公開している [[DefinedTerm/ai-ide]] である。[[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] が調査対象として選んだ 5 つのツールの 1 つであり、選定の根拠は、いずれのツールも、コード生成やチャットでのやり取りの際に IDE が従わなければならない [[DefinedTerm/ai-ide-rules]] を開発者が明示的に定義できることだった。同研究は、ツールの公式の変更履歴に基づき、そのリリース日を 2024 年 11 月 13 日と記録している。

## 機能

Windsurf のルールファイルは、プロジェクト内の `.windsurf/rules/` 以下に置かれる。単一ファイル形式の `.windsurfrules` もサポートされていたが、これは後にディレクトリベースの仕組みに置き換えられた。この配置場所と、ルールが生成とチャットの際に尊重されるという点を除けば、ここで用いている情報源は、この仕組みを Windsurf 独自の実装として説明するのではなく、5 つのツールすべてに共通する一般的なものとして特徴づけている ― 共通の説明については [[DefinedTerm/ai-ide-rules]] を参照。

## 導入とエコシステム

同研究には導入状況に関わる数値が 2 つあり、それぞれ異なるものを測っている。リポジトリのマイニングでは、最初の検索で Windsurf の候補プロジェクトが 3684 件返されたが、キーワードとルールファイルによるフィルタリングと手作業での確認を経て、AI IDE で構築されたと明言している 83 プロジェクトからなる最終データセットに残ったのは 5 件だった。実務者へのサーベイでは、回答者 99 人のうち 23 人が、現在開発に Windsurf を使用していると回答した。マイニングの数値は、このツールを使用し、かつそのことを README や説明文に記載している公開プロジェクトの数を反映しており、同研究は、AI IDE を使用していてもそれを明言していないプロジェクトは数えられていないと指摘している。一方、サーベイの数値は、ルールファイルへの変更をコミットしたことのある開発者の自己申告による使用状況を反映している。

実務者による利用体験の記録である [[BlogPosting/assessing-internal-quality-while-coding-with-an-agent]] は、Windsurf と Sonnet 3.5 を使って既存の Swift 製 Mac アプリケーションに機能を追加し、実装の前に作業の各まとまりについて計画を求めた経験を述べている。著者は、この組み合わせによってコードを書く速度は上がったものの、プロンプトによる入念な計画と、ビルド・テスト・デバッグのための Windsurf と Xcode の間の絶え間ない切り替えが必要だったこと、生成されたコードに重大な品質上の問題があったこと、そしてエージェントが問題を修正しようとして行き詰まりがちだったことを見いだし、全体としてあまり得るものがあるとは感じなかった。同じ記録の中で、後に [[SoftwareApplication/claude-code]] と Sonnet 4.5 で試みた際にはずっとうまくいき、著者はそのツールを日常的に使うようになった。
