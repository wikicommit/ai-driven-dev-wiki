---
title: "CodAGE"
type: "schema:Dataset"
lang: ja
tags: [エージェント, ソフトウェアリポジトリマイニング]
translated_from: ".wikicommit/entity/en/Dataset/codage.md"
source_commit: "c044ecf40b811dd9fe94970a2c89786a7a0bda4f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Coding Agent-generated GitHub Events。AI コーディングエージェントに帰属する GitHub イベントを GHArchive から収集した公開データセットで、プルリクエスト、レビュー、レビューコメントなどを扱うイベント種別ごとのサブセットに分かれている。"
  url: "https://huggingface.co/datasets/taher-ghaleb/CodAGE"
---

CodAGE（Coding Agent-generated GitHub Events）は、AI コーディングエージェントに帰属する GitHub イベントを集めた公開データセットである。[[ScholarlyArticle/ai-to-ai-code-reviews-of-github-pull-requests]] のソースデータとして用いられており、同研究はエージェントが作成しエージェントがレビューしたプルリクエストの母集団をこのデータセットから抽出している。

## 内容

データセットは複数のイベント種別サブセットに分かれている。上記の研究が利用した 3 つは、プルリクエストの作成者シグネチャを含む CodAGE-PRs と、レビュアー側の活動を含む CodAGE-Reviews および CodAGE-ReviewComments である。

その規模は、同研究が利用したスナップショットについて報告している件数からうかがえる。CodAGE-PRs に対する広範な第 1 段階の帰属判定では、暫定的なエージェントラベルの付いた候補プルリクエストが 4,563,819 件得られ、レビュー側の 2 つのストリームには 4,141,598 件のレビューイベントと 8,560,919 件のレビューコメントが含まれていた。

この第 1 段階にはブランチ名による証拠も含まれる。上記の研究はその後、同じ母集団に対するより厳格な第 2 段階として独自の 2 層シグネチャフレームワークを適用した。これは本文中のシグネチャまたはベンダーが管理するログインを必須とし、ブランチ名のみによる一致は除外するもので、これにより 450 万件の候補 PR が 2,830,284 件のエージェント作成と帰属される PR に絞り込まれた。同研究は、両段階とも自らのものであるため、両者の比較は外部検証ではなく内部の整合性チェックであると注記している。

## 来歴

CodAGE は GHArchive から収集されているため、対象は公開された GitHub イベントであり、プライベートリポジトリ、GitHub Enterprise のデプロイメント、その他のバージョン管理プラットフォームは含まれない。Hugging Face 上の <https://huggingface.co/datasets/taher-ghaleb/CodAGE> で CC BY 4.0 のもとで公開されている。

上記の研究が利用したスナップショットは 2024 年 1 月 1 日から 2026 年 4 月 15 日までを対象としている。同研究は、このスナップショットを扱ううえでの時期に関する 2 つの点を指摘している。対象期間は該当する時期をカバーしているものの、多くの自律型 AI コーディングエージェントが登場したのは 2025 年初頭になってからであること、そして GHArchive の帰属情報はイベントデータから約 1 四半期遅れるため、直近の四半期の件数は下限値となることである。

## 利用

[[ScholarlyArticle/ai-to-ai-code-reviews-of-github-pull-requests]] は、このデータセットを用いて [[DefinedTerm/closed-loop-ai-review]]（ある AI コーディングエージェントが作成し、別の AI コーディングエージェントがレビューしたプルリクエスト）のデータセットを構築した。同研究は、AI に帰属するレビューを少なくとも 1 件受けたエージェント作成の PR が 248,641 件あったと報告し、レビュアーの出力が作成エージェントによって、また同一製品同士か異なる製品間かの組み合わせによってどう変わるかを測定している。
