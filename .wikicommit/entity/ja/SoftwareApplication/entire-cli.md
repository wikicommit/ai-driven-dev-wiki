---
title: "Entire CLI"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングエージェント, CLI, オープンソース, エージェントツーリング]
translated_from: ".wikicommit/entity/en/SoftwareApplication/entire-cli.md"
source_commit: "09becb4eb728528ea1c24b3c450ca9da552891a4"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Entire.io によるオープンソースのコマンドラインツール。リポジトリ内のコーディングエージェントのセッションを自動的に記録し、どの行を人間が書き、どの行をエージェントが書いたかを行単位で帰属させたうえで、コードのコミットと紐づける。"
  applicationCategory: "開発者ツール"
  featureList: "コーディングエージェントのセッショントランスクリプトの記録、コミットに紐づくチェックポイント、人間とエージェントの行単位でのコード帰属"
---

Entire CLI は Entire.io によるオープンソースのツールであり、開発者がリポジトリで有効にすると、コーディングエージェントのセッショントランスクリプトを自動的に記録し、人間が書いた行とエージェントが書いた行を行単位で帰属させたうえで、結果として生じたコードのコミットと紐づける。SWE-chat の著者らによれば、このツールは、AI が生成した貢献をレビューし、理解し、検証することがますます難しくなっているという問題に対処するものである。開発者は、コードベースがどのように変化してきたかをコミット単位だけでなくプロンプト単位でも追跡でき、AI 支援によるあらゆる変更の検索可能な記録が作られる。このツールは 2026 年 2 月 10 日に一般公開された。

## 機能

CLI はリポジトリに git フックをインストールし、複数のコーディングエージェント（[[SoftwareApplication/claude-code]]、OpenCode、[[SoftwareApplication/gemini-cli]]、[[SoftwareApplication/cursor]]、Factory AI Droid）のセッショントランスクリプトを記録する。最初にサポートされたのは Claude Code である。ログには、ユーザーのプロンプト、エージェントの応答、ファイル編集・シェルコマンド・コード検索といったツール呼び出し、そしてトークン使用量が記録される。トランスクリプトは、チェックポイントとセッションのメタデータとともに、リポジトリの専用ブランチ（`entire/checkpoints/v1`）に保存され、各チェックポイントはコミットに紐づけられる。帰属はコミット時に、シャドウブランチ上の一時的なチェックポイントを用いて計算され、これによりコミットされた行が人間とエージェントのどちらによるものかの内訳が得られる。

## 導入とエコシステム

このチェックポイントブランチを公開 GitHub リポジトリにプッシュした開発者は、自身のセッションを誰でも読める状態にすることになり、これが [[Dataset/swe-chat]] の基盤となっている。そのデータ収集パイプラインは、GitHub のコード検索でそうしたリポジトリを見つけ、チェックポイントのディレクトリをダウンロードし、生のトランスクリプトを解析する。付随する研究である [[ScholarlyArticle/swe-chat-coding-agent-interactions-from-real-users-in-the-wild]] では、執筆時点でこのツール自身のリポジトリが占めるセッションの割合は 20% 未満であり、著者らは公開後に導入が広がるにつれてその割合が低下していると報告している。
