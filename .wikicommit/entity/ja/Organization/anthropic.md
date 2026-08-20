---
title: "Anthropic"
type: "schema:Organization"
lang: ja
tags: [エージェンティックコーディング, コンテキストエンジニアリング]
review_status: pending
translated_from: ".wikicommit/entity/en/Organization/anthropic.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Claude モデル群と [[SoftwareApplication/claude-code]] を手がける企業であり、[[DefinedTerm/model-context-protocol]] の出自でもある。[[DefinedTerm/context-engineering]] とエージェンティックコーディングに関する実践者向けの文章を数多く公開している。"
  url: "https://www.anthropic.com/"
---

Anthropic は Claude ファミリーのモデルと、そのエージェンティックコーディングツールである [[SoftwareApplication/claude-code]] を手がける企業である。製品と並行して、コーディングエージェントがどう使われているかについてのエンジニアリング文書や業界予測を公開しており、そのためエージェンティックコーディング領域のベンダーであると同時に、その語彙を実践者に供給する最も目につく出所の一つでもある。

## 沿革

ここで取り込んだ出典は Anthropic の創業や企業としての沿革を扱っていない。それらが記録しているのは、2024年後半以降のエージェンティックコーディングに関する同社の産出物である。

出典が記録する最も古い出来事は、2024年11月25日の [[DefinedTerm/model-context-protocol]] の発表である。これは Anthropic において [[Person/david-soria-parra]] と [[Person/justin-spahr-summers]] によって作られ、AI アシスタントをデータの所在するシステムへ接続するための標準としてオープンソース化された。2025年12月、Anthropic はこのプロトコルを [[Organization/agentic-ai-foundation]]——Block および [[Organization/openai]] とともに共同設立した Linux Foundation 傘下の指定基金——へ寄贈した。同月の後半には、エージェントがオンデマンドで読み込むタスク固有の指示とリソースをパッケージ化するための姉妹オープン標準として、同じオープン標準のアプローチに従って [[DefinedTerm/agent-skills]] を公開した。

## 活動と成果物

エージェント設計に関するエンジニアリング文書は「Engineering at Anthropic」の名のもとで公開されている。2025年9月29日に同社の Applied AI チームが公開した [[TechArticle/effective-context-engineering-for-ai-agents]] は、[[DefinedTerm/context-engineering]] はプロンプトエンジニアリングの自然な発展形であるという同社の立場を提示し、長期にわたるタスクに対して [[DefinedTerm/compaction]]、構造化されたノートテイキング、サブエージェントアーキテクチャを処方している。同記事はいくつかの技法を、Claude Code がそれらをどう実装しているかに即して記述しており、あらかじめ読み込まれる `CLAUDE.md` と併せて glob と grep によるジャストインタイムのファイル取得なども含まれる。

同社は予測も公開している。[[Report/2026-agentic-coding-trends-report]] は2026年のエージェンティックコーディングについて8つのトレンドを予測し、社内の調査結果を報告している。そこには Societal Impacts チームによる、開発者は業務のおよそ 60% で AI を使いながら「完全に委譲できる」タスクは 0〜20% にすぎないと答えているという知見が含まれる。同レポートはまた、エンジニアリング以外での Anthropic 自身の Claude Code の社内利用についても記述している——法務チームが契約書のレッドライン作業とコンテンツレビューのために Claude を用いたワークフローを構築し、コーディング経験のない弁護士がセルフサービスのトリアージツールを作った、というものである。

これらのうち最も広く波及しているのはプロトコルに関する取り組みである。[[BlogPosting/introducing-the-model-context-protocol]] は MCP を仕様と SDK、Claude デスクトップアプリにおけるローカルサーバのサポート、そしてサーバのオープンソースリポジトリとともに出荷し、開発ツール企業である Zed、Replit、Codeium、Sourcegraph と並んで Block と Apollo を早期採用者として挙げている。その1年後、Adam Jones と Conor Kelly による [[TechArticle/code-execution-with-mcp]] は、その普及が何を代償としたのかを取り上げた。エージェントが数百から数千のツールに接続されると、すべての定義をあらかじめ読み込み、中間結果をモデルを通して受け渡すことが過剰なトークンを消費するのである。そこで提案された答えが [[DefinedTerm/code-execution-with-mcp]] であり、ある事例のワークフローを 150,000 トークンから 2,000 トークンへ削減したと報告している。

Anthropic は、自社のプロトコルに関する第三者のセキュリティ研究にも登場する。[[Report/model-context-protocol-security]] は、その著者たちが推奨事項を実践的で実装可能なものに保つために Anthropic および MCP のメンテナコミュニティと協働していると述べ、編集者、寄稿者、技術運営委員会の共同議長のなかに Anthropic 所属の人々を挙げている。

これらの文章で言及されている開発者向けのプラットフォーム機能には、Claude Developer Platform でパブリックベータとして公開されたメモリツールとコンテキスト管理機能、そして軽量なコンパクションの一形態としてのツール実行結果のクリアがある。
