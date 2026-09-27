---
title: "Claude Developer Platform におけるコンテキスト管理"
type: "schema:BlogPosting"
lang: ja
tags: [コンテキストエンジニアリング, 長時間稼働エージェント, メモリ]
translated_from: ".wikicommit/entity/en/BlogPosting/managing-context-on-the-claude-developer-platform.md"
source_commit: "f948f309cb907fd940528e22bdf1a82e1e673130"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Claude Developer Platform 上の 2 つのコンテキスト管理機能を発表した、Anthropic による 2025 年 9 月の告知。コンテキストウィンドウが埋まるにつれて古くなったツール呼び出しとその結果をクリアするコンテキスト編集と、会話をまたいで永続するクライアントサイドのファイルストアであるメモリツールを紹介している。"
  datePublished: "2025-09-29"
  publisher: "[[Organization/anthropic]]"
---

この記事は、エージェントのコンテキストを管理するための Claude Developer Platform 上の 2 つの機能、[[DefinedTerm/context-editing]] とメモリツールを紹介している。出発点は本番環境での課題である。複雑なタスクをこなしてツールの結果を蓄積していくエージェントは、実効的なコンテキストウィンドウを使い果たしがちで、開発者はエージェントのトランスクリプトを切り詰めるか、性能の低下を受け入れるかの選択を迫られる。記事は 2 つの機能をこれに対する相補的な答えとして提示する。一方は関連するデータだけをコンテキストに残し、もう一方は価値ある情報をセッションをまたいで保持する。

[[Organization/anthropic]] はこの 2 つを Claude Sonnet 4.5 と同時にリリースした。同社によれば、Claude Sonnet 4.5 は会話を通じて利用可能なトークンを追跡することで、組み込みのコンテキスト認識（context awareness）を備えている。両機能は Claude Developer Platform 上、および Amazon Bedrock と Google Cloud の Vertex AI を通じてパブリックベータとして発表された。

## 要点

- コンテキスト編集は、コンテキストウィンドウがトークンの上限に近づくと、古くなったツール呼び出しとその結果を自動的にクリアし、会話の流れは保持する。記事によれば、これによりエージェントが手動介入なしに稼働できる時間が延び、Claude が関連するコンテキストだけに集中するため、実効的なモデル性能も向上する。
- メモリツールは、ファイルベースの仕組みを通じて、Claude がコンテキストウィンドウの外に情報を保存し参照できるようにする。Claude は、会話をまたいで永続する専用のメモリディレクトリ内のファイルを作成・読み取り・更新・削除できる（[[DefinedTerm/structured-note-taking]] を参照）。
- メモリツールはツール呼び出しを通じて完全にクライアントサイドで動作し、ストレージのバックエンドは開発者自身のインフラストラクチャ上にある。そのため、データをどこにどのように永続化するかは開発者が制御できる。
- 記事が示すユースケース別の役割分担は次のとおりである。コーディングでは、コンテキスト編集が古いファイルの読み取り結果やテスト結果をクリアし、メモリはデバッグで得た知見やアーキテクチャ上の決定を保持する。リサーチでは、メモリが主要な発見を保存し、古い検索結果はクリアされる。データ処理では、中間結果がメモリに送られ、生データはクリアされる。
- Anthropic は、エージェント型検索に関する社内評価セットにおいて、メモリツールとコンテキスト編集を組み合わせるとベースラインに比べて性能が 39% 向上し、コンテキスト編集単体では 29% 向上したと報告している。
- 100 ターンのウェブ検索評価では、コンテキスト編集により、コンテキストの枯渇によって本来なら失敗していたワークフローをエージェントが完了できるようになり、同時にトークン消費量が 84% 削減されたと報告している。

## 文脈

これはベンダーによる製品発表であり、性能の数値は Anthropic 自身の社内評価によるものである。この記事が紹介する 2 つの機能は、本 wiki が別の箇所でより詳しく扱っている手法に対応している。トランスクリプトからツールの結果をクリアする手法（[[DefinedTerm/tool-result-clearing]]）と、エージェント型メモリ（[[DefinedTerm/structured-note-taking]]）であり、どちらも [[TechArticle/context-engineering-memory-compaction-and-tool-clearing]] で [[DefinedTerm/compaction]] と比較されている。
