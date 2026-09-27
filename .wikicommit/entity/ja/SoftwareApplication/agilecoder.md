---
title: "AgileCoder"
type: "schema:SoftwareApplication"
lang: ja
tags: [マルチエージェント, コーディングエージェント, ソフトウェアプロセス]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/agilecoder.md"
source_commit: "0905902793f108bf59d40f17ccaecab6d323e38b"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "アジャイルのロールを担う LLM エージェントが、ユーザー要件から連続するスプリントを通じてソフトウェアを構築するマルチエージェントのソフトウェア開発フレームワーク。コンテキスト取得のためにコード依存グラフを最新の状態に保つ Dynamic Code Graph Generator がこれを支える。"
  applicationCategory: "マルチエージェントのソフトウェア開発フレームワーク"
  featureList: "アジャイルのロール（Product Manager、Scrum Master、Developer、Senior Developer、Tester）、受け入れ基準を伴うプロダクトバックログとスプリントバックログ、計画・開発・テスト・レビューからなるスプリント、3 段階の静的コードレビュー、コード依存グラフから導出されるテストスイートとテスト計画、Dynamic Code Graph Generator、メッセージストリームとグローバルメッセージプールを伴うインストラクターとアシスタントの対話"
---

AgileCoder は、アジャイル方法論を LLM エージェントに適用したマルチエージェントのソフトウェア開発フレームワークであり、そのリポジトリは <https://github.com/FSoft-AI4Code/AgileCoder> とされている。ユーザー要件が与えられると、アジャイルのロールを担うエージェントがスプリントを重ねながら段階的にソフトウェアを計画し、書き、レビューし、テストする。各スプリントの終わりには、フレームワークが納品するか次のスプリントを計画するかを決める。このフレームワークは
[[ScholarlyArticle/agilecoder-dynamic-collaborative-agents-for-software-development-based-on-agile-methodology]]
で導入された。著者らはこれを、ウォーターフォールモデルに従っていると彼らが説明する
[[SoftwareApplication/metagpt]] や [[SoftwareApplication/chatdev]] といったマルチエージェントシステムに対する代替として提示している。

## 機能

Product Manager がユーザー要件を開発タスクと受け入れ基準からなるプロダクトバックログに変換し、Scrum Master がその実現可能性をレビューする。その後、各スプリントは 4 つのフェーズで進む。計画フェーズでは、タスクが選ばれてスプリントバックログに入る。開発フェーズでは、Developer が docstring 付きのコードを書き、Senior Developer がそれを 3 段階で静的にレビューする。すなわち、空のメソッドや import の欠落といった基本的な実装のチェック、スプリントバックログへの準拠、そしてバグがなく受け入れ基準を満たしていることの確認である。テストフェーズでは、Tester がそのスプリントで変更されたファイルとその祖先ファイルに対するテストスイートを書き、テスト計画に従ってファイルを実行し、バグやテストの失敗があれば Developer に報告する。レビューフェーズでは、Product Manager が蓄積されたレポートをバックログと受け入れ基準と比較して終了するかどうかを決め、終了する場合は Scrum Master がソフトウェアの実行方法とライブラリのインストール方法に関するドキュメントを書く。

Dynamic Code Graph Generator は、ノードがコードファイルで、エッジが主に import 関係を表す Code Dependency Graph を保持し、コードの変更に合わせてそれを更新する。このグラフは、どのファイルにテストが必要かを決め、トポロジカル順序を逆にすることで論理的なテスト順序を与え、実行エラーが発生した場合には、エージェントがトレースバックからさかのぼって、コードベース全体ではなく関連するファイル横断のコンテキストだけを取得できるようにする。Execution Environment がコードを実行し、トレースバックをエージェントに返す。

エージェントは、インストラクターとアシスタントによる 2 者間の対話で、制約のない自然言語を用いてやり取りし、合意に達するかやり取りの上限に達するまで続ける。メッセージストリームが対話のワーキングメモリとして機能し、グローバルメッセージプールがすべての対話の出力と各タスクの状態を保存する。各対話はそこから自分に関係する部分だけを読み取る。

## 採用とエコシステム

論文では、GPT-3.5 Turbo、Claude 3 Haiku、GPT-4 をバックボーンモデルとして AgileCoder を実行し、HumanEval、MBPP、そして著者らがまとめたソフトウェア開発タスクのセットである [[Dataset/projectdev]] で評価している。著者らは、ペアプログラミング、CI/CD、カンバン、リーンといったさらなるアジャイルのプラクティスによる拡張や、ソフトウェア開発以外の領域へのこの手法の適用を提案している。
