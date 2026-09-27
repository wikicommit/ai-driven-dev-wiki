---
title: "AI コーディングツールにおけるエンジニアリング上の落とし穴：Claude Code、Codex、Gemini CLI のバグに関する実証研究"
type: "schema:ScholarlyArticle"
lang: ja
tags: [コーディングエージェント, ソフトウェア信頼性, 実証研究]
translated_from: ".wikicommit/entity/en/ScholarlyArticle/engineering-pitfalls-in-ai-coding-tools.md"
source_commit: "e3a247123c2e2c5a1d19244743218b709c140afd"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Claude Code、Codex、Gemini CLI のオープンソースリポジトリで公開報告された 3.8K 件を超えるバグを手作業で分析し、AI 支援コーディングツールを構築する際のエンジニアリング上の落とし穴を明らかにした実証研究。"
  author: ["Ruixin Zhang", "Wuyang Dai", "Hung Viet Pham", "Gias Uddin", "Jinqiu Yang", "Song Wang"]
  datePublished: "2026-03-21"
  keywords: ["AI コーディングツール", "バグ研究", "実証的ソフトウェアエンジニアリング", "コーディングエージェント"]
---

この論文は、[[SoftwareApplication/claude-code]]、Codex、[[SoftwareApplication/gemini-cli]] といった AI 支援コーディングツールのエンジニアリングを研究対象とする。論文は、これらのツールは大きな生産性向上を約束する一方で、従来のソフトウェアエンジニアリング、AI システム設計、ヒューマンコンピューターインタラクションの交差点に位置するそれらを構築することには、独特でまだよく理解されていない課題が数多く伴うと論じ、そこに関わるエンジニアリング上の落とし穴についての初の実証研究であると位置づけている。

著者らは、これら 3 つのツールのオープンソースの GitHub リポジトリで公開報告された 3.8K 件を超えるバグを、体系的かつ手作業で分析している。オープンコーディングの手法を用いて、各イシューの記述を関連するユーザーの議論や開発者の応答とあわせて調べ、すべてのバグを種類、発生箇所、根本原因、観察された症状によって分類している。このアノテーションは、よく見られる失敗パターンや繰り返し現れるエンジニアリング上の課題を明らかにするために用いられ、著者らはそれを、より信頼性の高い AI コーディングアシスタントを設計する開発者のためのロードマップとして提示している。

## 要点

- 調査対象のバグの 67% 超は機能に関連するものである。
- 根本原因の観点では、バグの 36.9% が API、統合、または設定の誤りに起因する。
- 最もよく観察される症状は、API エラー（18.3%）、ターミナルの問題（14%）、コマンドの失敗（12.7%）である。
- バグは主に、システムのワークフローのうちツール呼び出し（37.2%）とコマンド実行（24.7%）の段階に影響している。
- これらの数値はすべて、Claude Code、Codex、Gemini CLI という 3 つのツールのリポジトリで公開報告されたイシューから得られたものである。

## 補足

この論文は 2026 年 3 月 21 日に arXiv に投稿され、Software Engineering（cs.SE）に分類されている。
