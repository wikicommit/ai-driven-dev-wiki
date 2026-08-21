---
title: "Anthropic"
type: "schema:Organization"
lang: ja
tags: [エージェンティックコーディング, コンテキストエンジニアリング]
review_status: pending
translated_from: ".wikicommit/entity/en/Organization/anthropic.md"
source_commit: "d672e84e628c54abd484416debe97370df38bc4c"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Claude モデル群と [[SoftwareApplication/claude-code]] を擁する企業であり、[[DefinedTerm/model-context-protocol]] の発祥であり、[[DefinedTerm/context-engineering]] とエージェンティックコーディングについての実践者向けの文章を数多く公表している。"
  url: "https://www.anthropic.com/"
---

Anthropic は Claude ファミリのモデルと、そのエージェンティックコーディングのツールである [[SoftwareApplication/claude-code]] を擁する企業である。製品と並んで、コーディングエージェントがどう使われているかについてのエンジニアリングの文章と業界予測を公表しており、そのことが同社を、エージェンティックコーディングの領域におけるベンダーであると同時に、その実践者の語彙のより目立つ供給源の1つにしている。

## 沿革

ここで取り込まれた情報源は Anthropic の創業や企業としての沿革を扱っておらず、2024年終盤以降のエージェンティックコーディングに関する同社の産出物を記録している。

情報源が記録する最も古い出来事は、2024年11月25日の [[DefinedTerm/model-context-protocol]] の発表である。これは Anthropic で [[Person/david-soria-parra]] と [[Person/justin-spahr-summers]] によって作られ、AI アシスタントをデータのある場所と接続するための標準としてオープンソース化された。2025年12月、Anthropic はこのプロトコルを [[Organization/agentic-ai-foundation]]——Block と [[Organization/openai]] とともに共同設立した Linux Foundation 傘下の指定基金——へ寄贈した。同月のうちに、エージェントが必要に応じて読み込むタスク固有の指示とリソースをパッケージ化するための、同じくオープン標準としての姉妹規格 [[DefinedTerm/agent-skills]] を、同じオープン標準のアプローチに従って公開した。Agent Skills の仕様のリポジトリは、標準の側からこのフォーマットの由来について同じ説明——もともと Anthropic によって開発され、その後オープン標準として公開された——を与え、その後ますます多くのエージェント製品に採用されており、より広いエコシステムからの貢献を受け入れていること、リポジトリのコードは Apache 2.0、ドキュメントは CC-BY-4.0 のもとにあることを記録している。

## 活動と成果物

エージェントの設計についてのエンジニアリングの文章は「Engineering at Anthropic」の名のもとに公表されている。2025年9月29日に同社の Applied AI チームが公開した [[TechArticle/effective-context-engineering-for-ai-agents]] は、[[DefinedTerm/context-engineering]] がプロンプトエンジニアリングの自然な発展であるという同社の立場を示し、長期にわたるタスクに向けて [[DefinedTerm/compaction]]、構造化されたメモの作成、サブエージェントのアーキテクチャを処方する。この投稿は複数の技法を、Claude Code がそれらをどう実装しているかに言及しながら記述しており、あらかじめ読み込まれる `CLAUDE.md` と並ぶ、glob と grep を通じたジャストインタイムのファイル取得もそこに含まれる。同じシリーズの第2の投稿である、Ken Aizawa による2025年9月11日の [[TechArticle/writing-effective-tools-for-agents]] は、同じ推論をエージェントに与えられるツールへ適用しており、その助言がどう作られたかについての同社の説明が注目に値する。その大半は、Anthropic 自身の社内のツール実装を Claude Code で繰り返し最適化することから生まれ、自社の社内ワークスペースに対して評価され、取り置いたテストセットが同社の研究者の書いた実装を上回る利得を示した、というものである。

同社は予測も公表している。[[Report/2026-agentic-coding-trends-report]] は2026年のエージェンティックコーディングについて8つのトレンドを予測し、社内の研究知見を報告している。そこには同社の Societal Impacts チームの仕事も含まれ、開発者が自らの仕事のおよそ 60% で AI を使う一方で、「完全に委譲できる」と報告するタスクは 0〜20% にとどまることを見出している。同レポートはまた、エンジニアリング以外での Anthropic 自身の Claude Code の社内利用も記述している——法務チームが契約の赤入れとコンテンツのレビューのために Claude を用いたワークフローを構築し、コーディングの経験がない弁護士がセルフサービスのトリアージのツールを作った、という例である。

プロトコルの仕事はこれらのなかで最も広く波及している。[[BlogPosting/introducing-the-model-context-protocol]] は MCP を、仕様と SDK、Claude Desktop アプリでのローカルサーバのサポート、そしてサーバのオープンソースのリポジトリとともに送り出し、初期の採用者として Block と Apollo を、開発ツールの企業として Zed、Replit、Codeium、Sourcegraph を挙げた。1年後、Adam Jones と Conor Kelly による [[TechArticle/code-execution-with-mcp]] は、その採用が何を要したかを扱った。エージェントが数百から数千のツールへ接続されると、すべての定義をあらかじめ読み込み、中間結果をモデルを通して渡すことが過剰なトークンを消費する。提案された答えは [[DefinedTerm/code-execution-with-mcp]] であり、ある例のワークフローを 150,000 トークンから 2,000 トークンへ減らしたと報告されている。

Anthropic は自社のプロトコルについての第三者のセキュリティの仕事にも登場する。[[Report/model-context-protocol-security]] は、著者らが Anthropic と MCP のメンテナのコミュニティと協働して推奨事項を実践的かつ実装可能に保っていると述べ、編集者、コントリビュータ、技術運営委員会の共同議長のなかに Anthropic 所属の人々を挙げている。

この文章群で言及されている開発者向けのプラットフォームの機能には、Claude Developer Platform でパブリックベータとして公開されたメモリツールとコンテキスト管理の機能、そしてコンパクションの軽量な形としてのツール結果のクリアが含まれる。
