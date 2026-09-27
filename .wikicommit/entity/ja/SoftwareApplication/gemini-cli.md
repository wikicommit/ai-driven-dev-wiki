---
title: "Gemini CLI"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール, CLI]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/gemini-cli.md"
source_commit: "f98378c1c0274db465979eeb9b19989edbed4da1"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Gemini モデルを搭載した Google のターミナルベースの AI コーディングアシスタント。対話型のシェルセッションからコードベースに対して計画立案やコーディングを行うために使われる。Google は 2026 年 6 月 18 日以降、一般消費者向けユーザーへの提供を終了し、それらのユーザーは Antigravity CLI に移行すると発表したが、エンタープライズ利用と有料 API 経由の利用は継続される。"
  applicationCategory: "コマンドライン型コーディングアシスタント"
  author: "[[Organization/google]]"
---

Gemini CLI は [[Organization/google]] のコマンドラインアシスタントであり、同社の Gemini モデルを搭載し、AI エージェントを開発者のターミナルに持ち込む。開発者はシェルセッションからこれにプロンプトを与え、コードベースを分析させたり解決策の計画を起草させたりしたうえで、各ステップを指示しながら結果を対話的に反復改善していく。Google は 2025 年にこれをリリースし、2026 年 5 月にはターミナルエージェントの取り組みを [[SoftwareApplication/antigravity-cli]] に集約すると発表した。これにより Gemini CLI の一般消費者向けユーザーはそちらへ移行し、エンタープライズ顧客には引き続き Gemini CLI が提供される（[[BlogPosting/transitioning-gemini-cli-to-antigravity-cli]]）。

## 機能

コマンドラインから起動し、既存のコードベースに対して動作する。ある解説はコードベースの分析と解決策の計画の起草という 2 つの用途を挙げ、特徴として大きなコンテキストウィンドウを特筆しており、開発者は同じセッション内のやり取りを重ねながら出力を洗練させていく。Google 自身の説明では、機能として Agent Skills、フック、サブエージェント、拡張機能が挙げられ、ユーザーに好まれた点としてターミナル UI と週次のリリースサイクルが挙げられている。

Google Codelabs のワークショップ「AI Agent End to End」は、1 つのシステム構築全体を通じてこれを開発ツールとして使っている。このワークショップでは CLI のスラッシュコマンドが紹介されている。`/help`、`ReadFile`・`WriteFile`・`GoogleSearch` などの組み込みツールを一覧表示する `/tools`、エージェントが保持するコンテキストを確認・追加する `/memory show` と `/memory add` であり、さらにプロンプト内で `@` 記号を使ってファイルを参照する方法も示されている。ワークショップの説明によれば、`gemini` コマンドを実行するとカレントディレクトリにある `gemini.md` ファイルを探し、それがプロジェクト固有の指示マニュアルとして機能する。このファイルではペルソナを設定したり、ファイルや検索を指し示したり、プロジェクトで覚えておくべき事実やルールを保持したりできる。後のステップでは、コーディングガイドラインを `GEMINI.md` ファイルに書き込み、設計ドキュメントから CLI にエージェントを生成させており、これをコンテキストエンジニアリング的な作業の進め方として提示している。その後、CLI を使ってプロンプトから Google の [[SoftwareApplication/agent-development-kit]] 向けのエージェント、エージェント評価ファイル、デプロイスクリプト、CI/CD パイプラインを生成している。

## 採用とエコシステム

[[BlogPosting/future-of-agentic-coding-conductors-to-orchestrators]] は、人間が各ステップを指示し、ツールがセッション内で応答するという理由から、Gemini CLI を [[SoftwareApplication/claude-code]]、[[SoftwareApplication/cursor]]、IDE 内チャットアシスタントとともに指揮者（conductor）型のツールに分類している。この投稿はこれを、自ら勝手にコード変更を行うことのない一度に 1 つずつ作業する協働者として描いているが、これは論じている指揮者モードについて当てはまることであり、ツール全般についてではないと明示的に留保している。

移行について Google 自身が示した説明は、ユーザーのワークフローがこのツールの枠を超えて成長したというものである。ユーザーはいまや作業を分担するために互いに通信する複数のエージェントを求めており、そのためにはワークフローの他の部分とバックエンドを共有するターミナルツールが必要になる。Google は、2026 年 6 月 18 日に Gemini CLI と Gemini Code Assist の IDE 拡張機能が、Google AI Pro および Ultra の契約者と、個人向け Gemini Code Assist の無料ユーザーからのリクエストへの応答を停止すると発表した。Gemini Code Assist Standard または Enterprise ライセンスのもとで Gemini CLI を使っている組織は引き続きアクセスでき、Google は最新の Gemini モデルでサポートを続けると述べている。また、有料の Gemini API キーや Gemini Enterprise Agent Platform の API キーを通じて引き続き利用できる。Antigravity CLI は Gemini CLI の Agent Skills、フック、サブエージェントを引き継ぎ、拡張機能は Antigravity のプラグインになるが、Google は当初は機能が 1 対 1 で同等にはならないと述べている。
