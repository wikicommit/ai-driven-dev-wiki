---
title: "Safe-OS"
type: "schema:Dataset"
lang: ja
tags: []
translated_from: ".wikicommit/entity/en/Dataset/safe-os.md"
source_commit: "777a6f1fe30a4c2323cdc9454cdde1c69212981a"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "オンラインの OS エージェントに対するプロンプトインジェクション、システム妨害、環境攻撃からなる 100 例のベンチマーク。AgentBench の OS エージェントと Docker でシミュレートされた環境の上に構築されており、システム的なリスクのもとで LLM エージェントのガードレールを評価するために導入された。"
  creator: ["Weidi Luo", "Shenghong Dai", "Xiaogeng Liu", "Suman Banerjee", "Huan Sun", "Muhao Chen", "Chaowei Xiao"]
  url: "https://eddyluo1232.github.io/AGrail/"
  variableMeasured: ["description", "evaluation", "label", "user", "attack"]
---

Safe-OS は、ガードレールシステムがオンラインの OS エージェントに対するシステム的なリスクを検出できるかどうかを評価するための 100 例のベンチマークであり、[[ScholarlyArticle/agrail]] で [[DefinedTerm/agrail]] とともに導入された。AgentBench の OS エージェントと Docker ベースのシミュレート環境の上に構築されており、アクセス制御違反を現実的に表現できるよう、sudo 権限を持つ root ユーザーと持たない一般ユーザーという 2 つの異なるユーザー ID を割り当てるように拡張されている。

## 内容

各レコードは AgentBench の OS エージェント用データ形式に従う（自然言語による説明、Docker 内で実行される任意の初期化／開始用 Bash スクリプト、マッチベースまたはコードベースの評価チェック、そして操作を行うユーザーや、攻撃の場合は攻撃タイプのラベルと注入されたガード要求の原則といったメタデータ）。100 例の内訳は、一般的な LLM ジェイルブレイク戦略から作られたシステム妨害攻撃 30 例（例：フォーク爆弾を実行させるプロンプト）、無害な通常タスクの例 27 例、環境依存の攻撃 20 例（意図しないファイルの上書きのように、アクションのテキストだけからは特定できず周囲の環境に依存するリスク）、そしてプロンプトインジェクション攻撃 23 例（OS エージェントが読み込むファイル、パス、環境変数に隠された悪意ある指示）である。すべてのコマンドは、GPT-4o または GPT-4-Turbo を用いた OS エージェントに対して実行可能であることが手作業で検証されており、著者らは、自分たちのレッドチーム攻撃、プロンプトインジェクション攻撃、環境攻撃がいずれも GPT-4-Turbo に対して 90% 以上の攻撃成功率を達成すると報告している。

## 来歴

このデータセットは AGrail の著者らによって構築された。既存の OS エージェント向け安全性データセットは、LLM が生成した合成テストケースに頼りすぎており、現実世界のシナリオを十分に反映していないと判断したためである。Safe-OS の攻撃シナリオは、その代わりに、GPT-4 ベースの OS エージェントに対して過去に報告された成功した攻撃に基づいて設計されている。Docker でシミュレートされた OS 環境で動作し、AGrail プロジェクトの一部として <https://eddyluo1232.github.io/AGrail/> で公開されている。

## 用途

これを導入した論文 [[ScholarlyArticle/agrail]] は、Safe-OS を用いて [[DefinedTerm/agrail]] とベースラインの防御エージェンシー（LLaMA-Guard3、GuardAgent、AgentMonitor、ToolEmu）を、攻撃検出の精度（攻撃成功率が低いほど良い）と過剰防御（無害な通常シナリオの活動がどれだけブロックされるか）の両面で評価している。Claude-3.5-Sonnet ベースの AGrail は、無害なアクションの 96% を維持しながら、攻撃成功率をシステム妨害攻撃で 3.8%、プロンプトインジェクション攻撃で 0% に低減したと報告されている。これに対し、ベースラインの中には無害なアクションの 49% 超をブロックしたものもあった。
