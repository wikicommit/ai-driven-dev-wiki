---
title: "τ-bench"
type: "schema:Dataset"
lang: ja
aliases: ["tau-bench"]
tags: [エージェント評価, ベンチマーク, ツール利用]
translated_from: ".wikicommit/entity/en/Dataset/tau-bench.md"
source_commit: "918f7af409eaecc35e50dea8e21fc3277faf15bf"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "ツール・エージェント・ユーザー間の対話を評価するベンチマーク。言語モデルがシミュレートするユーザーと、ドメイン固有の API ツールおよびポリシーガイドラインを備えた言語エージェントとの動的な会話を模擬する。当初は航空会社（airline）と小売（retail）のドメインを対象としていた。"
  creator: ["Shunyu Yao", "Noah Shinn", "Pedram Razavi", "Karthik Narasimhan"]
  url: "https://github.com/sierra-research/tau-bench"
---

τ-bench（"tau-bench"）は、現実世界のドメインにおけるツール・エージェント・ユーザー間の対話のためのベンチマークである。言語モデルによってシミュレートされるユーザーと、ドメイン固有の API ツールおよびポリシーガイドラインを与えられた言語エージェントとの間の動的な会話を模擬する。そのリポジトリは GitHub の sierra-research オーガニゼーション配下にあり、MIT ライセンスで公開されていて、2024 年の論文（arXiv 2406.12045）で導入されたベンチマークのコードとデータを収録している。

## 内容

元のリポジトリには、航空会社（airline）と小売（retail）の 2 つの環境が含まれ、それぞれが独自のタスクを持つ。また、エージェント戦略 — 関数呼び出し（"tool-calling"）、Act、ReAct — を採点するリーダーボードがあり、k = 1〜4 の pass^k 指標が報告されている。現在リポジトリには、これらの airline と retail のタスクは古いバージョンであるという警告が掲げられている。後継の τ²-bench は τ³-bench へと更新されており、airline と retail のタスクを修正したうえで、銀行（banking）ドメインと音声評価モダリティを追加している。利用者は最新版としてそちらを参照するよう案内されている。

## 出自

このベンチマークはソースコードから、モデルプロバイダーの API に対して実行される。シミュレートされるユーザーはデフォルトで GPT-4o を `llm` 戦略で用いるが、代替のユーザーシミュレーター戦略も用意されている。`react` はシミュレートされたユーザーに応答の前に思考（thought）を書かせる。`verify` は LLM による検証ステップを追加し、不十分なユーザー応答を再生成する。`reflection` は不十分な応答についてシミュレーターに振り返り（reflection）をさせてから新たな応答を生成させる。実行には費用がかかることがあるため、リポジトリには両環境の過去の軌跡（trajectory）も同梱されており、さらなる軌跡の提供も呼びかけられている。

## 利用

失敗した実行の分析のために、リポジトリは LLM ベースの自動エラー特定ツールを提供している。このツールは失敗の責任（fault）をユーザー、エージェント、環境のいずれかに割り当て、その誤りを「部分的に達成されたゴール」「誤ったツール」「誤ったツール引数」「意図しないアクション」のいずれかに分類する。どちらのラベルにも説明が付される。リポジトリは、このツールが LLM に依存しているため、その特定結果は不正確な場合があると注意を促している。
