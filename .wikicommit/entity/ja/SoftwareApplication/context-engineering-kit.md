---
title: "Context Engineering Kit"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール, LLM, プロンプティング]
translated_from: ".wikicommit/entity/en/SoftwareApplication/context-engineering-kit.md"
source_commit: "d6b740fcefb776ad598c9c610d08c7220255d861"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "AI コーディングエージェント向けのコンテキストエンジニアリング・プラグインのマーケットプレイス。プロンプトパターンを、Claude Code、Gemini CLI、Antigravity、Cursor などのツール向けにインストール可能なスキル、コマンド、サブエージェントとしてパッケージ化している。"
  applicationCategory: "AI コーディングエージェント向けプラグインマーケットプレイス"
  featureList: "依存関係のないプラグイン単位のインストール、サブエージェントに支えられたコマンド指向のスキル、リフレクション・仕様駆動開発とサブエージェント駆動開発・レビュー・テスト・Git・ドキュメント・MCP セットアップにまたがる 13 のプラグイン、プロンプト中の「reflect」という語でリフレクションを起動するフック、コードレビューのための GitHub Actions 連携"
  author: "[[Organization/neolabhq]]"
---

Context Engineering Kit は、AI コーディングエージェント向けの [[DefinedTerm/context-engineering]] プラグインのマーケットプレイスであり、[[Organization/neolabhq]] が公開し、GPL-3.0 ライセンスのもとで公開 GitHub リポジトリから配布されている。このキットは自らを、最小限のトークン消費で済むよう手作業で作り込まれた高度なコンテキストエンジニアリングの手法とパターンの集まりであり、エージェントの結果の品質と予測可能性を高めることを目的としたもの、と説明している。対象は [[SoftwareApplication/claude-code]]、OpenCode、[[SoftwareApplication/cursor]]、Antigravity、その他のエージェントである。

キットの内容には 2 つの出所がある。プロジェクトによれば、このマーケットプレイスは開発者自身が長期間にわたって日常的に使ってきたプロンプトに基づいており、それを、ベンチマークで評価された論文や、プロジェクトが高品質と判断した他のプロジェクトから派生したプラグインで補っている。2 つ目のグループの背景にある研究については別途リストが公開されており、改良ループ、メモリの統合とキュレーション、原則に基づく批評、評価パターン、マルチエージェント討論、構造化された探索、段階的な推論と検証、ハルシネーションの低減を扱っている。

配布されるのは実行可能なソフトウェアではなくプロンプト素材である。すなわち、エージェントが自身のコンテキストに読み込むスキル、スラッシュコマンド、ルール、サブエージェント定義である。プロジェクトは、そのスキルが [agentskills.io](https://agentskills.io) の仕様に従っていること、そして Spec-Driven Development プラグインが用いる仕様テンプレートが arc42 ドキュメント標準に基づき、LLM が扱える形に調整されたものであることを述べている。

## 機能

このキットは単一のバンドルとしてではなくマーケットプレイスとしてインストールされ、プロジェクトはその粒度を設計目標の 1 つとして扱っている。各プラグインは自身のエージェント、コマンド、スキルだけを読み込むため、ユーザーは必要なものだけをインストールできる。Claude Code では `/plugin marketplace add NeoLabHQ/context-engineering-kit` でマーケットプレイスを追加する。この時点では何もコンテキストに読み込まれずにプラグインが利用可能になり、その後、各プラグインを個別にインストールする（例：`/plugin install reflexion@NeoLabHQ/context-engineering-kit`）。

他のエージェントのサポートは粒度が粗く、プロジェクトはこの点をごまかさずに明言している。

- **Gemini CLI** はリポジトリを拡張機能としてインストールし、**Antigravity CLI** はリポジトリの `antigravity/` フォルダからインストールする。どちらもすべてのプラグインのスキルとエージェントを 1 つのバンドルとして取り込む。プロジェクトは、どちらの CLI もプラグイン単位の選択をサポートしていないと注記し、インストール後に不要なスキルを削除することを勧めている。
- **Cursor、Codex、OpenCode など**は `npx skills add` を通じてインストールし、個々のスキルを選択できる。ただし、これらのプロバイダーはそれぞれ独自のエージェント形式を用いており、このインストーラーはサブエージェントをサポートしていないため、プロジェクトはこの経路では完全な体験は得られないとしている。
- さらなる代替手段として OpenSkills も提供されている。

プラグイン自体はいくつかのグループに分かれる。Reflexion は、フィードバックと改良のループのための `/reflect`、`/memorize`、`/critique` を提供し、プロンプトに「reflect」という語が現れると自動的に `/reflect` を実行するフックも備えている。このフックには `bun` が必要だが、コマンド自体には不要である。Spec-Driven Development と Subagent-Driven Development は、[[DefinedTerm/spec-driven-development]] と [[DefinedTerm/subagent-driven-development]] で説明されている方法論を実装する。Review は、bug-hunter、code-quality-reviewer、contracts-reviewer、historical-context-reviewer、security-auditor、test-coverage-reviewer という 6 つの専門エージェントによるコードレビューとプルリクエストレビューを、影響度と確信度によるフィルタリング付きで提供する。プロジェクトはこれを、GitHub Actions でも実行できる CodeRabbit のオープンソース代替として位置づけている。残りのプラグインは、Git 操作、テスト駆動開発、Clean Architecture と SOLID のためのドメイン駆動開発（Domain-Driven Development）ルール、[[DefinedTerm/first-principles-framework]]、改善（Kaizen）式の根本原因分析、エージェント自身のコマンドとスキルの作成、ドキュメント作成、言語固有のルール、Model Context Protocol サーバーのセットアップを扱う。

## 採用とエコシステム

プロジェクトは、エージェントに与える足場（スキャフォールディング）の量と、完全に正確な結果を生み出す信頼性との関係を比較した資料を公開している。その範囲は、素のワンショットプロンプトから、リフレクション、ジャッジ役のサブエージェント、ファイルグループ単位の実行を経て、人間によるレビューを伴う文書化された仕様にまで及ぶ。その形そのものが主張となっている。この段階を進むにつれて信頼性は高まるが、トークンのオーバーヘッドもそれとともに増え、ワンショットプロンプトではゼロだったものが、仕様駆動の経路ではベースラインの数倍に達する。そして、変更されるファイル数が増えるほどその差は広がる。これらの数値はプロジェクト自身によるもので、独立したベンチマークではなく、本番プロジェクトでの 1 年以上にわたる実際の開発利用に基づくと説明されている。Spec-Driven Development プラグインに関する付随的な主張、すなわちチームがテストしたすべてのケースで動作するコードを生成したという主張も、同様に自己申告によるものである。

プロジェクトは、信頼性を志向する 3 つのプラグインを競合ではなく補完的なものとして位置づけており、それらの間の選択は信頼性とトークンコストのトレードオフであるとし、まず Subagent-Driven Development と Spec-Driven Development から始めることを推奨している。プロジェクトの他の 2 つのプロジェクトがコンパニオンとして紹介されている。1 つは Microsoft の公式 devcontainers イメージに基づくエージェント向けの開発用サンドボックスイメージである Agent Sandbox、もう 1 つはエージェントを複雑さの低い読みやすいコードへと導くことを意図した ESLint 設定である Agent Eslint Config である。どちらもキットとは独立して動作するとされている。
