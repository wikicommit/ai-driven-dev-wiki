---
title: "GitHub Copilot CLI"
type: "schema:SoftwareApplication"
lang: ja
aliases: ["Copilot CLI"]
tags: [コーディングエージェント, コーディングツール]
translated_from: ".wikicommit/entity/en/SoftwareApplication/github-copilot-cli.md"
source_commit: "7567a177e4f0172fd7847cc2fe9a076543e5ad54"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "GitHub のエージェント型コマンドラインツール。大規模言語モデルを呼び出すエージェントが、ターミナルからユーザーに代わって半自律的にコマンドを実行する。"
  applicationCategory: "エージェント型コマンドラインコーディングツール"
  author: "[[Organization/github]]"
---

GitHub Copilot CLI は、[[Organization/github]] によるエージェント型コマンドラインツールである。[[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]] の説明によれば、この種のツールは大規模言語モデルを呼び出すエージェントを活用し、コマンドラインからユーザーに代わって半自律的にコマンドを実行する。同論文はこれを [[SoftwareApplication/claude-code]] や [[SoftwareApplication/gemini-cli]] とともに、ソフトウェア開発者のあいだで人気が高まっているエージェント型コマンドラインツールとして分類している。これは [[SoftwareApplication/github-copilot]] の CLI 以外の形態、すなわち VS Code などの IDE におけるコード補完、チャット、エージェントモードとは別のものである。

## 機能

GitHub のある研究者が、これを使って社内向けのエージェントツールを構築した経緯を記した記事（[[BlogPosting/agent-driven-development-in-copilot-applied-science]]）は、Copilot CLI が提供する対話モードを示している。変更を加える前にエージェントと一緒に機能を詰めるための `/plan` コマンドと、合意した計画をエージェントが実装する `/autopilot` モードである。セッション内から、エージェントに [[SoftwareApplication/github-copilot-code-review]] へのレビュー依頼を出させ、その完了を待ち、関連するコメントに対応し、コメントがなくなるまでレビューを再依頼させることもできる。同じ記事は Copilot SDK を Copilot CLI を基盤とするものとして説明しており、それによってその上に構築されたエージェントは既存のツールや MCP サーバーにアクセスでき、新しいツールやスキルを登録する手段も得られる。

また、Copilot CLI は [[DefinedTerm/github-copilot-custom-agents]] を実行する。この機能に関する GitHub の記事（[[BlogPosting/custom-agents-in-github-copilot-cli]]）は、エージェントプロファイル（`.agent.md` で終わる Markdown ファイルで、YAML フロントマターによってエージェントの役割、スコープ、能力、ガードレールを定義する）をリポジトリの `.github/agents` ディレクトリに追加し、Copilot CLI から `/agent` スラッシュコマンドでそのエージェントを選択する方法を説明している。同記事は、Copilot CLI がすでにスクリプトを実行し、API を呼び出し、リポジトリを直接扱えることから、エージェント駆動の作業に適していると述べている。そのため、チームは実行中心のワークフロー（セキュリティ監査、Infrastructure as Code のコンプライアンスレビュー、リリースノート作成、インシデントの初動調査など）を一度定義しておけば、ターミナルから毎回同じ方法で実行できる。

## 採用状況とエコシステム

その採用について最も詳しい記録は、[[Organization/microsoft]] が 2026 年初頭に行った社内展開の研究から得られる。そこでは Copilot CLI は Claude Code と並ぶ、公認された 2 つのエージェント型コマンドラインツールの一つであり、Microsoft は一般提供前の製品プレビュープログラムを通じてこれを利用できた。採用資格のあるエンジニアのあいだでは、初回利用は主に社会的な接触を通じて広まった。スキップレベルの同僚やマネージャーがすでに使っていたエンジニアは、試す可能性が顕著に高かった。一方、展開前に IDE の Copilot に頼っていたエンジニアは、Copilot CLI を試す可能性は高かったものの、使い続ける可能性は低かった。

同研究における単一ツール利用者の個人内比較では、Copilot CLI を使った週にはマージされたプルリクエストが +24.9% 増加し、Claude Code の +11.4% を上回った。著者らは 2 つの仮説を示している。エンジニアが 2 つのツールを異なるタスクの組み合わせに使っていたというもの、そして Microsoft が GitHub を所有しているため、組織的な力が Copilot CLI のハーネスを Microsoft のエンジニアの働き方に合わせる方向に働いた可能性が高いというものである。研究期間の終了直後、社内告知により、Microsoft のエンジニアの大半の Claude Code ライセンスが打ち切られ、影響を受けるエンジニアは Copilot CLI へ誘導されることが示された。調査対象の開発者の一部は、Copilot CLI への移行を報告している。
