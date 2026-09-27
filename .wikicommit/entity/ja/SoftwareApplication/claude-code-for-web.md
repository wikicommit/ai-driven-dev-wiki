---
title: "Claude Code for web"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, Anthropic, コーディングツール, サンドボックス化]
translated_from: ".wikicommit/entity/en/SoftwareApplication/claude-code-for-web.md"
source_commit: "d3a6cc04042ea62012d6cdb8d9075c83b708d517"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Anthropic がホストする非同期型の Claude Code。Anthropic が管理するコンテナ内で GitHub リポジトリを対象に実行され、Web およびモバイルのインターフェースから操作する。完了するとブランチを作成し、オプションでプルリクエストも作成する。"
  applicationCategory: "非同期型コーディングエージェント"
  featureList: "ホストされたコンテナ内での GitHub リポジトリを対象とした実行、ネットワークアクセスなしからカスタムのドメイン許可リストまで選択可能なネットワーク環境、実行中に送信したプロンプトのキューイング、ブランチとオプションでのプルリクエストの作成、トランスクリプトと編集済みファイルのローカル CLI へのテレポート"
  author: "[[Organization/anthropic]]"
---

Claude Code for web は、[[SoftwareApplication/claude-code]] のホスト型・非同期型の形態であり、
Anthropic が 2025 年 10 月にリリースした。Claude の Web インターフェースから、また Claude の iPhone アプリの
タブとして利用できる。情報源が明確に立証しているのは、それが Anthropic の管理するコンテナ内で実行されるという
ことである。そのコンテナ内で何が動いているかについての特定は、著者自身が外側から推測したものとして示されている ―
著者が知る限りでは、コンテナに包まれ、パーミッションの確認をスキップするよう設定された Claude Code CLI であり、
著者はそれがローカルのツールとまったく同じように振る舞うように見えると報告している。

これは非同期型コーディングエージェントのカテゴリーに属し、情報源はこれを OpenAI の Codex Cloud や
[[SoftwareApplication/google-jules]] に対する Anthropic の対抗製品として位置づけており、その形も非常によく似ている。
リポジトリを指定し、プロンプトを与え、作業の様子を見守るのではなく、結果をブランチとして受け取るのである。

## 機能

実行は、エージェントに GitHub リポジトリを指定し、環境を選び、プロンプトを与えることで設定される。実行中にも
追加のプロンプトを送ることができ、それらはキューに入れられて現在のステップが完了した後に実行される。実行が
終わると、エージェントは作業内容を含むブランチをリポジトリ上に作成し、オプションでプルリクエストを作成することも
できる。「テレポート」機能は、チャットのトランスクリプトと編集されたファイルの両方をローカルの Claude Code CLI に
コピーするため、ホスト環境で始めたセッションをローカルで引き継ぐことができる。

環境の選択はセキュリティに関わる制御であり、情報源は、完全にロックダウンされた設定から、制限されたドメインの
許可リストを経て、すべてを許可する `*` を含むユーザーが選んだドメインを許可する設定までの幅を説明している。
情報源が環境を明示している唯一の実行は、その幅の開放側の端にあるもの ― カスタムの `*` 許可リストのもとで
プライベートリポジトリを対象に行ったベンチマーク ― であり、そのプロジェクトには保護が必要な秘密情報もソースコードも
含まれていなかったためにその設定が選ばれた。それとは別に、情報源はネットワークアクセスなしで実行すれば何も心配する
ことはないと述べ、中間の設定のデフォルトの許可リストについては不安を記している。

## 注記

情報源の評価では、これが生成するプルリクエストはローカルの CLI によるものと区別がつかない ― 同じプロンプトを
ノートパソコン上で与えてもおそらく同じ結果になっただろうと報告している ― とされ、製品の価値は完全に利便性、
すなわち Anthropic が管理するホスト型コンテナとその上の Web およびモバイルのインターフェースにあるとしている。
挙げられている例は、単一ファイルの小さなツール、README の修正、そしてグラフまで備えた複数シナリオの Python
テンプレートエンジンのベンチマークであり、最後のものはスマートフォンのキーボードで入力された。

コストについては、情報源は一般化を避けており、Anthropic からテスト用に提供されたプランを使っていたことを記し、
自身の日々の CLI の利用額を非公式のツールで見積もるにとどめている。

## 関連

[[SoftwareApplication/claude-code]], [[DefinedTerm/sandboxing]], [[DefinedTerm/lethal-trifecta]], [[SoftwareApplication/google-jules]], [[SoftwareApplication/openai-codex]], [[BlogPosting/claude-code-for-web-async-coding-agent]]
