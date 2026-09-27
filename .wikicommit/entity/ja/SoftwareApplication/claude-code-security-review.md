---
title: "Claude Code Security Review"
type: "schema:SoftwareApplication"
lang: ja
tags: [セキュリティ, コードレビュー, claude-code]
translated_from: ".wikicommit/entity/en/SoftwareApplication/claude-code-security-review.md"
source_commit: "f948f309cb907fd940528e22bdf1a82e1e673130"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Anthropic による Claude Code 向けの自動セキュリティレビュー。ターミナルからその場で分析を行う /security-review コマンドと、新しいプルリクエストごとにレビューを行い、見つけた脆弱性にインラインでコメントする GitHub Action として提供されている。"
  applicationCategory: "自動セキュリティコードレビュー"
  featureList: "Claude Code の /security-review コマンド、新しいプルリクエストをトリガーとする GitHub Action、SQL インジェクション・XSS・認証と認可の欠陥・安全でないデータ処理・依存関係の脆弱性をカバーするセキュリティ特化のプロンプト、誤検知や既知の問題を除外するカスタマイズ可能なルール、推奨される修正を添えた PR のインラインコメント"
  author: "[[Organization/anthropic]]"
---

Claude Code Security Review は、[[Organization/anthropic]] による [[SoftwareApplication/claude-code]] 向けの自動セキュリティレビューであり、2025 年 8 月に [[BlogPosting/automate-security-reviews-with-claude-code]] で発表された。この名前は、発表記事がこれらの機能のドキュメントへのリンクに用いているものである。記事自体は自動セキュリティレビューを 2 つの形態で説明している。開発者がターミナルから Claude Code で実行する `/security-review` コマンドと、プルリクエストに対して実行される GitHub Action である。どちらの形態でも、Claude にコード内のセキュリティ上の懸念を特定させ、その後それらを修正するよう依頼することができる。

これは、開発者が AI に頼ってより速くリリースし、より複雑なシステムを構築するようになるにつれて、コードのセキュリティがより重要になるという懸念に応えるものである。Anthropic はこれを、[[DefinedTerm/security-code-review]] を既存のワークフローに組み込み、脆弱性が本番環境に到達する前に検出されるようにする手段として位置づけている。

## 機能

`/security-review` コマンドは、コードがコミットされる前にその場で分析を実行する。Claude はコードベースから潜在的な脆弱性を探し、見つけたものについて詳細な説明を与える。このコマンドは、一般的な脆弱性パターンをチェックするセキュリティに特化したプロンプトを使用し、その対象には SQL インジェクションのリスク、クロスサイトスクリプティング、認証と認可の欠陥、安全でないデータ処理、依存関係の脆弱性が含まれる。その後、Claude Code に各問題の修正を実装するよう依頼できる。このコマンドは Claude Code を最新バージョンに更新することで利用可能になり、カスタマイズすることもできる。

GitHub Action は、プルリクエストが作成されると自動的にトリガーされ、変更内容をセキュリティ上の脆弱性についてレビューし、カスタマイズ可能なルールを適用して誤検知や既知の問題を除外し、推奨される修正とともに各懸念を説明するインラインコメントをプルリクエストに投稿する。

## 採用とエコシステム

Anthropic は両方の機能をすべての Claude Code ユーザーが利用できるものとして発表しており、このアクションは既存の CI/CD パイプラインと統合でき、チームのセキュリティポリシーに合わせてカスタマイズできると説明している。Anthropic は Claude Code 自体を含む自社のコードにこのアクションを使用していると報告しており、プルリクエストがマージされる前、あるいはコードがリリースされる前にそれが脆弱性を検出した 2 つの例を挙げている。ローカルの HTTP サーバーを起動する社内ツールにおける DNS リバインディングを通じて悪用可能なリモートコード実行の脆弱性と、社内の認証情報を管理するために構築されたプロキシにおける SSRF の脆弱性である。
