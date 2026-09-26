---
title: "マルチモデルオーケストレーション"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント, マルチエージェント, オーケストレーション]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/multi-model-orchestration.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "複数のプロバイダーのモデルをベースにしたコーディングエージェントを 1 つのオーケストレーションのもとで動かし、各モデルの特性に応じて役割を分担させること。"
---

マルチモデルオーケストレーションとは、複数のプロバイダーのモデルをベースにしたコーディングエージェントを 1 つの
オーケストレーションのもとで動かし、各モデルの特性に応じて作業を分担させる実践である。
[[BlogPosting/sdd-in-unity-client-antipatterns-and-improvements]] はこれを、スループットの上限に対する解決策として
説明している。単一プロバイダーのトークン消費上限によって並列に走らせられる作業ラインの数が頭打ちになっていたが、
作業を複数のプロバイダーに分散させることでその上限が引き上げられたという。

## 用法

同記事の構成では、[[SoftwareApplication/claude-code]] がメインエージェント、[[SoftwareApplication/openai-codex]]
がサブエージェントである。仕様は Opus で書かれ、実行は Sonnet と GPT-5.3-Codex で行われる。仕様実装コマンドは、
実装、テストの作成、一般的な作業を Codex に一括で委任し、Claude がその結果を仕様への適合という観点でレビュー
する。Codex が何度も失敗した場合や回帰テストが失敗した場合には、Claude Code が作業を引き取り、自ら実装する。

Codex CLI はスキルを介してシェルから呼び出され、JSON を返す。成功時にはタスクの出力、使用トークン数、ログ
ディレクトリを、失敗時には終了コード、使用トークン数、ログディレクトリ、そして Codex が提案する修正を返す。
Codex に再度問い合わせるのは失敗時のみであり、そのログに基づく提案が Claude に渡される。

## 適用される場面

同記事は、単一プロバイダーのトークン上限が並列のエージェント作業を頭打ちにしている場合にこれを適用している。
モデル間でのコンテキストの分断を橋渡しする手段が前提となる。サブエージェントはメインエージェントのコンテキストを
共有しないため、Claude が仕様から Codex 向けのプロンプトを生成する。また著者は、Codex には Claude よりも厳密な
指示が必要だと気づいたため、Codex に適したプロンプトを組み立てる専用のスキルを用意している。報告されている
問題点は 2 つある。コンテキストがモデル間で断片化すること、そしてメインエージェントが効率を理由に Codex への
委任を避ける理由を挙げることがあることである。後者について著者は完全には抑制できておらず、作業ログを通じて
監視している。これは 1 人のエンジニアによる 1 つのプロジェクトでの報告であり、記事のまとめもこれを測定結果と
してではなく、スループットを高める有効な手段として提示している。

## 関連用語

- [[DefinedTerm/sub-agent-architecture]]
- [[DefinedTerm/context-bloat-loop]]
- [[DefinedTerm/deterministic-quality-gate]]
