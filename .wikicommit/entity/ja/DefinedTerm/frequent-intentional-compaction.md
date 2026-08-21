---
title: "頻繁で意図的なコンパクション"
type: "schema:DefinedTerm"
lang: ja
tags: [コンテキストエンジニアリング, コンパクション, エージェンティックコーディング, 用語]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/frequent-intentional-compaction.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "コンテキストウィンドウが 80〜100% 埋まってから事後的にコンパクションするのではなく、各フェーズの境界で予防的にコンパクションを行い、使用率を 40〜60% の帯に保つ手法。"
  termCode: "FIC"
  inDefinedTermSet: ""
---

頻繁で意図的なコンパクション——FIC と略される——は、コンテキストウィンドウがほぼ埋まるまで待つのではなく、ワークフローの各フェーズ境界で意図的かつ頻繁に [[DefinedTerm/compaction]] を実行する実践である。[[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] はこれを [[DefinedTerm/research-plan-implement]] ワークフローを特徴づける要素として説明し、HumanLayer に帰している。

## 用法

掲げられている運用上の目標は、コンテキスト使用率を 40% から 60% のあいだに保つことである。この技法が対置されているのは、80〜100% まで埋まってから慌ててコンパクションすることだ。コンパクションは、品質がすでに劣化してからの緊急対応としてではなく、予防的かつ頻繁に行われる。

そのサーベイが伝える報告された成果は、30 万行の Rust コードベースにおいて、このアプローチによってチームが1週間分の仕事を1日で完了できたというものである。この数字は独立した測定ではなく HumanLayer 自身の報告に由来する。

Research → Plan → Implement のサイクルは各フェーズ境界ですでに永続的な成果物——`research.md`、`plan.md`、進捗ファイル——を生み出しているため、その地点でのコンパクションは比較的安全である。そうでなければウィンドウから失われていたものが、すでにディスクへ書き出されているからだ。これは、サーベイが長時間セッションのあらゆるパターンに共通して見出している「永続ストレージとしてのファイルシステム」という原則そのものである。

## 関連用語

FIC は異なる機構ではなく [[DefinedTerm/compaction]] のためのスケジューリングの規律であり、サーベイが提示する [[DefinedTerm/context-rot]] への2つの答えのうちの一つである——もう一つはセッションを短く保ち、各フェーズ境界で新たに始め直すことだ。フェーズごとの成果物への依存は、これを [[DefinedTerm/agentic-memory]] と結びつける。そして、FIC が管理するコンパクションのリスクは、[[DefinedTerm/governance-decay]] が安全制約のレベルで記録しているものと同じである。
