---
title: "GitHub Copilot"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール]
translated_from: ".wikicommit/entity/en/SoftwareApplication/github-copilot.md"
source_commit: "a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "もともと Codex をベースに開発され、GitHub のコードリポジトリで学習された AI ペアプログラミングツール。複数のプログラミング言語にわたってコンテキストを考慮したコード補完を提供し、Visual Studio Code や JetBrains の IDE などのエディタに緊密に統合されている。"
  applicationCategory: "IDE のコード補完アシスタント"
  author: "[[Organization/github]]"
---

GitHub Copilot は、もともと Codex をベースに開発され、GitHub のコードリポジトリで学習された AI ペアプログラミングツールである。複数のプログラミング言語にわたってコンテキストを考慮したコード補完を提供し、Visual Studio Code や JetBrains といった一般的な IDE に緊密に統合されている。

## 機能

AI エージェント型プログラミングに関するサーベイは、素の GitHub Copilot を*反応型*に分類している。ユーザーのプロンプトに直接応答する（開発者が関数のヘッダーを入力すると、即座に関数本体を提案する）だけで、独立したタスク計画を行わず、テストの作成や生成されたコードの確認といった次のステップにも進まない。

同サーベイで例示されているアーキテクチャとツールカタログは別の対象に属するものであり、[[SoftwareApplication/github-copilot-coding-agent]] で説明している。その図 1 は Copilot そのものではなく *GitHub Copilot 風の*エージェント型プログラミングシステムを図示したものであり、サポートされるツールの表は GitHub Copilot agent についてのものとしてキャプションが付けられている。

## 採用状況とエコシステム

同サーベイは比較分類の中で、素の GitHub Copilot を反応型の「IDE アシスタント」に分類している。個々のプロンプトに応答する（開発者が関数のヘッダーを入力した後、即座に関数本体を提案するなど）だけで、インタラクションをまたいで状態やメモリを保持しない。デフォルトのコンテキストウィンドウは 16,000 トークンで永続的なメモリを持たず、アクティブな編集バッファ上のスライディングウィンドウを使うと報告している。サーベイはこれを、GitHub Copilot 自身のより自律的でマルチターンの「エージェント」モードとは別の製品として扱っている。[[SoftwareApplication/github-copilot-coding-agent]] を参照。

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] は、GitHub Copilot が人間とエージェントのやり取りをプルリクエストに結びつけ、エージェントの提案とその結果としてのコード変更の永続的な履歴記録を作り出すことから、トレーサビリティへの対応においてコマンドラインのエージェント型プラットフォームより先行していると述べている。同論文は、それでも残る課題も指摘している。Copilot はエージェントへのメンタリングとコードを互いに結びつかない別々の成果物として扱うため、コード変更をロールバックしても、それを生み出したエージェントの状態や会話スレッドはロールバックされず、特定のメンタリングとそのコードへの具体化とのあいだの因果的なつながりは明示的に保持されない。

GitHub 自身の製品発表は、素の Copilot を、同社が製品群を通じて描くはしごの一段に位置づけている。コード補完、次の編集の提案、チャット、エージェントモード、そしてバックグラウンドで動く [[SoftwareApplication/github-copilot-coding-agent]] であり、これらはすべて開発者をフロー状態に保つという単一の使命のもとに置かれている。GitHub は Universe 2025 で、プラットフォームの新規開発者の 80% が最初の 1 週間で Copilot を使っていると報告した。

このサブスクリプションは、[[SoftwareApplication/agent-hq]] の販売経路でもある。GitHub は、Anthropic、OpenAI、Google、Cognition、xAI のコーディングエージェントが、有料の Copilot サブスクリプションの一部として GitHub 内で直接利用できるようになると表明した。あわせて、組織の Copilot ユーザーがどのエージェントやモデルを利用できるかを管理するエンタープライズ向けのコントロールプレーンと、組織全体の Copilot の利用状況を報告するメトリクスダッシュボードも提供される。これらのパートナーエージェントのうち最初にエディタに届いたのは [[SoftwareApplication/openai-codex]] で、発表の週に VS Code Insiders の Copilot Pro+ ユーザー向けに提供された。
