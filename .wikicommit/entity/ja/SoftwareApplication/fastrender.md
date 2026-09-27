---
title: "FastRender"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングエージェント, マルチエージェント, 長時間稼働エージェント]
translated_from: ".wikicommit/entity/en/SoftwareApplication/fastrender.md"
source_commit: "7eb1cf131af15d0a15cbf2c12619cd499ed31158"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "長時間稼働エージェントのスケーリングに関する Cursor の実験において、大規模な自律型コーディングエージェント群がゼロから構築した実験的な Web ブラウザ。1,000 ファイルにわたり 100 万行を超えるコードから成ると報告されている。"
  applicationCategory: "Web ブラウザ（実験的）"
---

FastRender は、ほぼ全体が自律型コーディングエージェントによって書かれた実験的な Web ブラウザであり、同時に稼働する大規模なコーディングエージェント群をどこまで推し進められるかを探る [[SoftwareApplication/cursor]] の実験のテストケースとして作られた。Simon Willison が引用した Cursor 自身の説明によれば、Cursor はこのシステムに Web ブラウザをゼロから構築するという目標を与え、エージェントは 1 週間近く稼働し、1,000 ファイルにわたって 100 万行を超えるコードを書いた。ソースコードは GitHub で公開されている。

エージェントは、タスクを作成するプランナーとサブプランナー、それを実行するワーカー、そして各サイクルの終わりにプロジェクトが完了したかどうかを判断するジャッジエージェントという構成で組織されていた。Willison はこの構造を [[SoftwareApplication/claude-code]] がサブエージェントを使う方法になぞらえた。この構造については [[DefinedTerm/planner-worker-model]] でより詳しく説明されている。

## 機能

Willison はリポジトリの README にあるビルド手順に従って macOS 上で FastRender をビルド・実行し、動作するブラウザウィンドウを得た。google.com と自身のブログを表示したスクリーンショットでは、ページは読める状態でおおむね正しかったものの、スタイルの当たっていないボタン、文字化けしたタブ名、位置のずれた装飾用の引用符といった明らかなレンダリングの不具合があった。彼はこうした不具合を、このプロジェクトが既存のレンダリングエンジンを単にラップしたものではない証拠と受け止めた。リポジトリには WhatWG と CSS-WG のさまざまな仕様が Git サブモジュールとして含まれており、彼はこれを、エージェントが必要としうる参照資料を確実に手元に置くための賢いやり方だと評した。

## 導入とエコシステム

最初の発表は懐疑的に受け止められた。とりわけ、プロジェクトの GitHub Actions による CI が失敗しており、リポジトリにビルド手順がないことが明らかになってからはそうであった。ビルド手順はその後まもなく追加された。2029 年までに誰かが主に AI の支援によって本格的な Web ブラウザを構築するだろうと予測していた Willison は、FastRender は自分が想定していた成果の品質に近いと書いた。ただし、この種のプロジェクトが近いうちに Chrome、Firefox、WebKit と競合するとは考えていない。彼は、AI 支援コーディングで本格的なブラウザを構築する試みを 2 週間のうちに見たのはこれが 2 例目だと述べている。
