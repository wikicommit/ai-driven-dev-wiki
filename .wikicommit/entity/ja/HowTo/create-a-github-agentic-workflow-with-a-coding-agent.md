---
title: "コーディングエージェントで GitHub Agentic Workflow を作成する"
type: "schema:HowTo"
lang: ja
tags: [エージェント, CI/CD, エージェントツーリング]
review_status: pending
translated_from: ".wikicommit/entity/en/HowTo/create-a-github-agentic-workflow-with-a-coding-agent.md"
source_commit: "ec1aed6cc815a0de19917c1c3fa9646b24090b11"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "コーディングエージェントに自然言語でワークフローを説明して GitHub Agentic Workflow を作成するための、GitHub が文書化した手順。エージェントが Markdown のワークフローを書き、そのロックファイルをコンパイルし、コミット前に両方をレビューのために返す。"
  tool: ["GitHub CLI", "gh aw 拡張機能", "サポートされているコーディングエージェントの CLI"]
---

この手順は、リポジトリを [[SoftwareApplication/github-agentic-workflows]] 用にセットアップし、そのうえで平易な言葉による説明からコーディングエージェントにワークフローを書かせ、コンパイルさせ、コミットさせるものである。GitHub のチュートリアルは、変更に十分なテストがあるかを確認する自動プルリクエストレビュアーを例に手順を説明しており、関連するハウツーでは、Issue として届けられる日次または週次のリポジトリ活動レポートを例に説明している。GitHub は、Agentic Workflows はパブリックプレビュー段階であり、変更される可能性があるとしている。

## 前提条件

- GitHub Actions が有効で、自分が書き込み権限を持つリポジトリ。
- インストールと認証を済ませた GitHub CLI 2.0.0 以降。ドキュメントに記載されたログインコマンドは `gh auth login --scopes repo,workflow` である。
- サポートされているコーディングエージェントとその認証情報へのアクセス。チュートリアルでは Claude Code、OpenAI Codex、Google Gemini CLI、Copilot CLI が挙げられている。

## 手順

1. GitHub CLI 用の Agentic Workflows 拡張機能をインストールする: `gh extension install github/gh-aw`。GitHub CLI 2.90.0 以降では、拡張機能がない場合、任意の `gh aw` コマンドを実行するとインストールを促される。
2. ワークフローを実行するエンジンを選び、その認証情報を利用可能にする。[[SoftwareApplication/claude-code]]、[[SoftwareApplication/openai-codex]]、[[SoftwareApplication/gemini-cli]] の場合は、対応する API キー（`ANTHROPIC_API_KEY`、`OPENAI_API_KEY`、`GEMINI_API_KEY`）を、Settings → Secrets and variables → Actions からリポジトリシークレットとして保存する。Copilot CLI はデフォルトのエンジンである。組織が所有するリポジトリでは、ワークフローのフロントマターの `permissions` に `copilot-requests: write` を追加すれば別途シークレットは不要だが、個人のリポジトリでは、Copilot Requests を Read に設定した fine-grained personal access token を格納した `COPILOT_GITHUB_TOKEN` シークレットが必要になる。組織への課金にする場合は、さらに組織の管理者が、組織の Copilot ポリシー設定で「Allow use of Copilot CLI billed to the organization」ポリシーを有効にする必要がある。
3. リポジトリのルートで `gh aw init` を実行する。これにより、コーディングエージェントがワークフローを作成・編集するのを助けるスキルと指示が追加される。
4. リポジトリでコーディングエージェントのセッションを開始する。たとえば Claude Code、OpenAI Codex、Gemini CLI、[[SoftwareApplication/github-copilot-cli]]、あるいは VS Code のエージェントモードである。
5. ワークフローの説明を添えて `agentic-workflows` スキルを呼び出す。例: `/agentic-workflows create a pr reviewer that ensure the changes are tested.` エージェントは `.github/workflows/` にワークフローの Markdown ファイルを作成し、対応する `.lock.yml` の GitHub Actions ワークフローをコンパイルして、両方をレビューしてコミットするよう求める。
6. 生成されたワークフローをレビューし、その後ファイルをコミットしてプッシュするようエージェントに依頼する。
7. 実行する。ワークフローは、リポジトリの Actions タブから、または `gh aw run YOUR-WORKFLOW-NAME` でトリガーできる。例のレビュアーはプルリクエストをトリガーとするため、プルリクエストを作成または更新すると実行され、完了すると、変更に十分なテストが含まれているかを記したプルリクエストレビューを残す。

## 補足

- その後のワークフローの保守も、同じ対話的なやり方で行う。GitHub は、レビュー基準の改善、チェックの追加、失敗した実行のデバッグを、自然言語でエージェントに依頼することを勧めている。
- ワークフローを手作業で更新するには、`.github/workflows/` にあるその Markdown ファイルを編集し、`gh aw compile` を実行してロックファイルを更新し、両方のファイルをコミットしてプッシュしたうえで、プルリクエスト上で GitHub Actions のチェックを確認する。
- 上記の 4 つ以外のエンジン、たとえば Pi という実験的なエンジンは、プロジェクト自身の認証リファレンスに掲載されている。
