---
title: "Jules Tools"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール, CLI, エージェントツーリング]
translated_from: ".wikicommit/entity/en/SoftwareApplication/jules-tools.md"
source_commit: "a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Google の非同期型コーディングエージェント Jules 向けの軽量なコマンドラインインターフェースおよび TUI。Jules をスクリプトから操作可能にし、他のターミナルツールと組み合わせられるようにする。"
  applicationCategory: "コーディングエージェント向けコマンドラインインターフェース"
  author: "[[Organization/google]]"
  featureList: "リモートの Jules セッションを操作するためのコマンドとフラグ、タスク用の TUI ダッシュボード、他の CLI ツールと組み合わせたスクリプトによる操作"
---

2025 年 10 月に発表された Jules Tools は、Google の非同期型コーディングエージェントである
[[SoftwareApplication/google-jules]] 向けの軽量なコマンドラインインターフェースである。それまで開発者が Jules を
主に Web ブラウザ経由で操作していたことから Google がこれを作ったのであり、ターミナルを離れることなくタスクを
立ち上げ、Jules が何をしているかを確認し、エージェントをカスタマイズする手段だと説明している。

Google はこれを、コーディングエージェントのためのダッシュボードであると同時にコマンドの操作面でもあるものとして
提示している。その意義として述べられているのはアクセスの利便性だけではない。Google は、この CLI によって Jules が
プログラム可能、スクリプト可能、カスタマイズ可能になり、開発者自身の自動化に組み込んだり、短いコマンドでエージェントを
リアルタイムに誘導したりできるようになると主張している。

## 機能

Google は、最も簡単な始め方として npm を挙げている。

```
npm install -g @google/jules
```

この CLI の中核は、Jules に何をさせるかを指示する**コマンド**と、その振る舞いを調整する**フラグ**を軸に構成されている。
Google が挙げる例は、リモートのタスクを一覧表示する `jules remote list --task` と、ライトテーマのターミナル
インターフェースに切り替える `jules --theme light` である。

スクリプトから操作できるため、Jules Tools は他のコマンドラインツールと組み合わせられる。Google が公開している例では、
Jules に接続されたリポジトリを一覧表示する、`jules remote new --repo <repo> --session "<task>"` で指定した
リポジトリに対してリモートセッションを作成する、`TODO.md` ファイルをループで回して 1 行ごとに 1 つのセッションにする、
`gh` から GitHub の issue タイトルをパイプで直接新しいセッションに渡す、Gemini CLI を使って一覧から最も面倒な issue を
選ばせて Jules に渡す、といったことが示されている。

対話的な利用のために、このツールは TUI も提供している。Google によれば、`/remote` などのコマンドでタスクの
ダッシュボード表示が得られ、`/new` ではタスクの作成を段階的に案内してくれる。Google はこれを、Web UI と同じ操作性を、
より速く、開発者がすでにローカルで作業している場所のより近くで提供するものだと特徴づけている。

## 採用状況とエコシステム

Google はこのツールを、開発ツールに対する「設計段階からのハイブリッド」という考え方の中に位置づけている。すなわち、
ローカルとリモートの併用（必要なときは開発者自身のマシンを使い、スケールが必要なときは複数の VM を立ち上げる）と、
自分でやることと委任することの併用（コードに直接関わり続けつつ、作業をエージェントに任せる）である。この発表と
その具体例は [[BlogPosting/meet-jules-tools]] に記述されている。
