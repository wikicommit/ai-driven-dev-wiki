---
title: "ProjectDev"
type: "schema:Dataset"
lang: ja
tags: [ベンチマーク, 評価, コード生成, マルチエージェント]
translated_from: ".wikicommit/entity/en/Dataset/projectdev.md"
source_commit: "0905902793f108bf59d40f17ccaecab6d323e38b"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "それぞれがプロンプトと要件リストからなる 14 のソフトウェア開発タスクの集まり。マルチエージェントシステムが完全で実行可能な複数ファイルのプログラムを生成できるかを評価するために、AgileCoder の著者らがまとめたもの。"
---

ProjectDev は、競技プログラミングの問題よりも複雑な 14 の代表的なソフトウェア開発タスクからなるセットであり、
マルチエージェントのソフトウェア開発システムを評価するために
[[ScholarlyArticle/agilecoder-dynamic-collaborative-agents-for-software-development-based-on-agile-methodology]]
の著者らがまとめたものである。各タスクは、テスト対象のシステムに対して、複数の実行可能ファイルからなる包括的な
コードベースを生成するよう求める。著者らはこれを、そうしたシステムの評価には HumanEval や MBPP よりも
適したものとして提示している。

## 内容

各タスクは、短いプロンプト（たとえば「Create a snake game」）と、ゲームボード、衝突処理、スコア計算、
エラー処理といった見出しの下にまとめられた詳細な要件リストで構成される。タスクは多様な領域にわたり、
ミニゲーム（スネーク、ブロック崩し、2048、Flappy Bird、戦車バトル、Caro）、Streamlit・pandas・SQLite の
上に構築されたデータ処理および CRUD アプリケーション、カスタムのプレスリリース生成ツール、動画プレーヤー、
YouTube 動画ダウンローダー、QR コードの生成・検出ツール、ToDo リストアプリ、電卓などが含まれる。

## 来歴

著者らは、コード生成ベンチマークと実世界のソフトウェア開発との間のギャップを埋めるために、タスクを自ら
収集したと説明している。また、公開されていないとする MetaGPT の SoftwareDev や ChatDev の SRDD とは
対照的に、このデータセットは一般公開される予定だと述べている。

## 利用

AgileCoder の論文では、各手法をタスクごとに 3 回実行し、得られたプログラムを Python 経験 2 年以上の
開発者が手作業で評価する。実行できたプログラムは、タスクの要件のうち満たした割合によってスコア付けされ、
実行に失敗したプログラムの数はエラーとして数えられる。これに基づき、同論文は
[[SoftwareApplication/agilecoder]] が [[SoftwareApplication/chatdev]] や
[[SoftwareApplication/metagpt]] よりも高い実行可能性を示したと報告している。
