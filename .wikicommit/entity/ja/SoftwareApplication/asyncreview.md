---
title: "AsyncReview"
type: "schema:SoftwareApplication"
lang: ja
tags: [コードレビュー, エージェントツーリング, サンドボックス化]
translated_from: ".wikicommit/entity/en/SoftwareApplication/asyncreview.md"
source_commit: "ebe0aa0633b147a8544f3ed123bd09c74adc6988"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "GitHub のプルリクエストとイシューを対象とする、オープンソースのエージェント型コードレビューツール。差分だけから推論するのではなく、Recursive Language Models を用いてリポジトリを探索し、コンテキストを取得し、回答する前にサンドボックスの中で指摘事項を検証すると自らを説明している。"
  applicationCategory: "コードレビューツール"
  featureList: "差分を超えたリポジトリの探索、検証のための Python REPL サンドボックス、GitHub API によるツール呼び出しのインターセプト、npx による実行、エージェントスキルとしてのインストール"
---

AsyncReview は、GitHub のプルリクエストとイシューに対してエージェント型コードレビューを行うオープンソースのツールである。自己紹介によれば、Recursive Language Models を用いて単純な差分解析の先へ進み、リポジトリを自律的に探索し、関連するコンテキストを取得し、回答する前に安全なサンドボックスの中で指摘事項を検証する。README は、DevinReview に着想を得たと述べている。

ドキュメントに記されたループは 5 つの段階からなる。エージェントが推論して計画を立て、Python コードを生成し、そのコードをモデルへのクエリやツールコマンドとともに Python REPL サンドボックスの中で実行し、ツール呼び出し ― README はファイルの取得と検索を挙げている ― はインターセプトされて GitHub API から応答が返され、その結果を観察して再帰的に繰り返す。

README がこの形を支持する論拠は、変更された行だけを読むツールとの対比である。README は 4 つの対を示している。限られたコンテキストに対して、依存関係を理解するためにリポジトリ内の任意のファイルを読むこと。コードの動作を推測する静的解析に対して、検索クエリや検証用スクリプトを実行すること。ライブラリのメソッドをでっち上げることに対して、実在するファイルパスと行を引用すること。そして一発での生成に対して、回答する前に反復することである。これはプロジェクト自身による代替手段の特徴付けであり、独立した比較ではない。README は評価もベンチマークも報告しておらず、唯一の性能に関する主張は定量化されていない。アーキテクチャ図の終点が「10x High Quality Answer」となっているだけである。

## 機能

このツールは `npx asyncreview review` によってインストールなしで実行でき、プルリクエストまたはイシューの URL と自由記述の質問を受け取る。Gemini の API キーが必要で、`GEMINI_API_KEY` として与える。プライベートリポジトリの場合はさらに GitHub のトークンが必要で、`GITHUB_TOKEN` として、または `--github-token` フラグを通じて与える。README は、トークンは GitHub CLI から取得できると記している。

直接呼び出す以外に、AsyncReview は他のエージェント型のプロバイダー ― README は Claude、Cursor、OpenCode、Gemini、Codex を挙げている ― からスキルとして使われるように設計されており、その理由として、これによりそれらのエージェントがローカルにアクセスできないコードベースを見て推論できるようになる、と述べている。その経路でのインストールは `npx skills add AsyncFuncAI/AsyncReview` であり、README によれば `vercel/skills` に対応したエージェントで動作する。手動でのセットアップでは、エージェントに `skills/asyncreview/SKILL.md` ファイルを指定する。バックエンドサーバーと Web インターフェースをローカルで実行することもでき、これはリポジトリ内で別途ドキュメント化されている。

## 採用とエコシステム

リポジトリは GitHub アカウント AsyncFuncAI によって MIT ライセンスのもとで公開されている。ファイル一覧は上で説明した複数のエントリーポイントを反映しており、`cli`、`npx`、`web`、`skills/asyncreview` の各ディレクトリが分かれている。

より大きな構図の中でこのプロジェクトが体現しているのは、スキルとしてパッケージ化された形の [[DefinedTerm/agentic-code-review]] である ― 差分を読むのではなくリポジトリの中で行動するレビュアーであり、単体のツールとしてだけでなく、別のコーディングエージェントがインストールして呼び出す機能としても提供されている。
