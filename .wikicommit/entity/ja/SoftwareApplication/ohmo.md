---
title: "ohmo"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, エージェントツーリング]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/ohmo.md"
source_commit: "abe7dbaa9cb573068b927bda52cc565d6ba058e6"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "OpenHarness 上に構築され、同じリポジトリで配布されている HKUDS のパーソナル AI エージェント。Feishu、Slack、Telegram、Discord などのチャットアプリを通じて対話し、既存の Claude Code または Codex のサブスクリプションで動作する。"
  applicationCategory: "パーソナル AI エージェント"
  author: "HKUDS"
---

ohmo は、[[SoftwareApplication/openharness]] 上に構築され、同じリポジトリで配布されているパーソナル AI エージェントである。README ではこれを「また一つのチャットボットではなく、長いセッションにわたって実際にあなたのために働くアシスタント」と説明している。ユーザーは Feishu、Slack、Telegram、Discord で ohmo とチャットし、ohmo は自らブランチを切り、コードを書き、テストを実行し、プルリクエストを作成する。既存の [[SoftwareApplication/claude-code]] のサブスクリプションまたは Codex のサブスクリプションで動作するため、追加の API キーは不要である。

## 機能

ohmo は `~/.ohmo` 以下に個人用のワークスペースを持ち、これは `ohmo init` で一度だけ作成する。そこにあるファイルには、エージェントの長期的な性格と振る舞い（`soul.md`）、ohmo が何者か（`identity.md`）、ユーザーのプロフィールと好み（`user.md`）、初回起動時のブートストラップの儀式（`BOOTSTRAP.md`）、個人用のメモリディレクトリ、そして選択したプロバイダープロファイルとチャネルを記録するゲートウェイ設定が収められている。`ohmo config` は、OpenHarness 自体のセットアップと同じワークフローの選択肢を使ってチャネルとモデルプロバイダーを設定し、変更後には実行中のゲートウェイを再起動できる。ゲートウェイはエージェントをチャットアプリにつなぐ役割を担い、コマンドラインから起動、フォアグラウンドでの実行、状態確認、再起動ができる。2026 年 4 月の OpenHarness のリリースで、ohmo のチャネルにチャネル用スラッシュコマンド、ファイル添付、マルチモーダルメッセージが追加された。
