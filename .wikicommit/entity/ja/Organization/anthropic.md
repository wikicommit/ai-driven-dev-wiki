---
title: "Anthropic"
type: "schema:Organization"
lang: ja
tags: [エージェント, LLM]
translated_from: ".wikicommit/entity/en/Organization/anthropic.md"
source_commit: "b0cc6ca63c7e8c23683ba90cc3b5cf0b4690d315"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Claude モデル、エージェント型コーディングツール Claude Code、Claude Developer Platform を手がける企業であり、Engineering at Anthropic ブログの発行元。"
  url: "https://www.anthropic.com/"
---

Anthropic は、Claude ファミリーのモデルと、それを基盤とするツール群を手がける企業である。ツールには、エージェント型コーディングソリューションの [[SoftwareApplication/claude-code]] や Claude Developer Platform が含まれる。同社は Engineering at Anthropic ブログを通じて、Claude 上でエージェントを構築するチームに向けたエンジニアリングのガイダンスを公開している。

同社の Applied AI チームは、実践におけるエージェント構築について執筆している。このチームが表明している立場は、[[DefinedTerm/context-engineering]] は [[DefinedTerm/prompt-engineering]] が自然に発展したものであり、コンテキストは埋め尽くすものではなく、厳選すべき有限の資源として扱うべきだというものである。この見解は [[BlogPosting/effective-context-engineering-for-ai-agents]] で示されている。Anthropic は、Claude の上にエージェントを構築するチームに対して、「うまくいく最も単純なことをせよ」を一貫した助言として掲げている。

長時間稼働エージェントに関するある記事は、Anthropic が公開しているエンジニアリング成果のうち、さらに 2 つを紹介している。1 つは自律的なフルスタック開発のための 2 エージェント構成のハーネス（プロジェクトを一度だけセットアップする初期化エージェントと、繰り返し起動されて段階的に作業を進め、テストを実行し、コミットするコーディングエージェント）であり、もう 1 つは [[SoftwareApplication/claude-managed-agents]] の背後にある [[DefinedTerm/brain-hands-session-split]] アーキテクチャである。同じ記事は、Claude のインスタンスが実際のオフィス向け自動販売ビジネスを 1 か月間運営した Anthropic の Project Vend を、エージェントが単一のセッションではなく数週間にわたって一貫したアイデンティティを維持しなければならない場合に何が起こるかを示した、初期の公開事例として紹介している。また、別の科学計算のケーススタディにも言及しており、そこでは Claude Opus 4.6 が数日かけてボルツマンソルバーを構築し、参照実装との一致度が 1% 未満の誤差に達したという。

## 活動と製品

- Claude ファミリーのモデル。
- 同社のエージェント型コーディングソリューションである [[SoftwareApplication/claude-code]]。
- Claude Developer Platform。Anthropic はこのプラットフォーム上で、ファイルベースの仕組みによってコンテキストウィンドウの外に情報を保存・参照するためのメモリツールをパブリックベータとして公開しているほか、ツール結果のクリア機能も提供している。
- 長時間稼働エージェント向けのホスト型ランタイムである [[SoftwareApplication/claude-managed-agents]]。
- Engineering at Anthropic。同社が開発者向けのガイダンスを公開しているブログ。
