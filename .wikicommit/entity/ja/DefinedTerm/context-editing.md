---
title: "コンテキスト編集"
type: "schema:DefinedTerm"
lang: ja
tags: [コンテキストエンジニアリング, コンテキストウィンドウ, 長時間稼働エージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/context-editing.md"
source_commit: "f948f309cb907fd940528e22bdf1a82e1e673130"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Claude Developer Platform 上のコンテキスト管理機能の一つで、エージェントのコンテキストウィンドウがトークン上限に近づいたときに、古くなったツール呼び出しとその結果を自動的に消去しつつ、会話の流れは保持するもの。"
---

コンテキスト編集（context editing）とは、[[Organization/anthropic]] が 2025 年 9 月に [[BlogPosting/managing-context-on-the-claude-developer-platform]] で Claude Developer Platform に導入した機能であり、エージェントのコンテキストウィンドウがトークン上限に近づいたときに、その中から古くなったツール呼び出しとその結果を自動的に消去する。もはや関係のない内容は取り除かれる一方で会話の流れは保たれる。Anthropic によれば、これにより人手の介入なしにエージェントが稼働し続けられる時間が延び、Claude が関連するコンテキストだけに注意を向けるようになるため、実効的なモデル性能も向上する。

## 用法

コンテキスト編集が対象とするのは、作業を進めるにつれてツールの結果を蓄積し、実効的なコンテキストウィンドウを使い果たしてしまうエージェントである。Anthropic はこの状況を、放っておけば開発者がエージェントのトランスクリプトを切り詰めるか性能の低下を受け入れるかの二者択一を迫られるものとして説明している。この機能は、会話をまたいで永続するクライアントサイドのファイルベースのストアであるメモリツール（[[DefinedTerm/structured-note-taking]]（構造化ノートテイキング）を参照）と同時に発表された。コンテキスト編集がアクティブなウィンドウを身軽に保ち、メモリはそのウィンドウを越えて残すべきものを保存する。Anthropic の例もこの二つを組み合わせている。コーディングでは古いファイル読み込みやテスト結果を消去しつつ、メモリにはデバッグで得た知見やアーキテクチャ上の決定を残す。リサーチでは古い検索結果を消去しつつ、メモリには重要な発見を残す。

発表に際して Anthropic 自身が示した評価の数値は次のとおりである。社内のエージェント型検索の評価セットでは、コンテキスト編集単独でベースラインより 29%、メモリツールと組み合わせると 39% 性能が向上した。また 100 ターンの Web 検索評価では、本来ならコンテキストの枯渇によって失敗していたはずのワークフローをエージェントが完了できるようにしつつ、トークン消費量を 84% 削減した。発表時点では、Claude Developer Platform 上と、Amazon Bedrock および Google Cloud の Vertex AI を通じてパブリックベータとして提供されていた。

古いツール結果をプレースホルダーに置き換えつつ、各呼び出しが行われたという記録は残すという具体的な操作については、[[DefinedTerm/tool-result-clearing]]（ツール結果の消去）でより詳しく扱っている。

## 関連用語

- [[DefinedTerm/tool-result-clearing]]
- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/compaction]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/context-rot]]
