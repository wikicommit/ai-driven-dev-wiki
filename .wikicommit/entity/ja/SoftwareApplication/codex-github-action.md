---
title: "Codex GitHub Action"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングエージェント, エージェントスキル, エージェント安全性]
translated_from: ".wikicommit/entity/en/SoftwareApplication/codex-github-action.md"
source_commit: "bcf2a6e3499612efcdde4e63a1d4d23bb9dc9e6f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "GitHub Actions のワークフロー内で Codex を実行するための OpenAI の GitHub Action。リポジトリローカルのスキルなど、ローカルで機能している Codex のワークフローを CI に持ち込むために使われる。"
  applicationCategory: "コーディングエージェントの CI 統合"
  featureList: "GitHub Actions のジョブのステップとしての Codex の実行、リポジトリローカルのスキルと AGENTS.md のルールの CI での再利用"
  author: "[[Organization/openai]]"
---

Codex GitHub Action は、GitHub Actions のワークフロー内で [[SoftwareApplication/openai-codex]] を実行する。[[BlogPosting/using-skills-to-accelerate-oss-maintenance]] において、[[SoftwareApplication/openai-agents-sdk]] のリポジトリのメンテナーたちは、これをローカルで有用になったワークフローを CI に持ち込むための部品として説明している。[[DefinedTerm/agents-md]] にあるリポジトリのポリシーがどのワークフローが必須かを Codex に伝え、リポジトリローカルのスキルがそれらのワークフローを保持し、この Action が同じプロセスを自動的に実行する。

## 機能

出典はこの Action を、そのインターフェースではなく用途によって説明している。Agents SDK のリポジトリでは、スキルに基づくワークフローを CI で自動化している。記事の例は JavaScript リポジトリの changeset 検証スキルで、その検証ルールは共有プロンプトに保持されており、ローカルでの実行と GitHub Actions が同じロジックを適用するようになっている。

公開リポジトリ向けに、記事はこの Action に関するセキュリティチェックリストを紹介している。ワークフローを開始できる者を制限すること、信頼できるイベントや明示的な承認を優先すること、PR・コミット・Issue・コメントから取り込むプロンプト入力をサニタイズすること、`drop-sudo` や非特権ユーザーを使って `OPENAI_API_KEY` を保護すること、そして Codex をジョブの最後のステップとして実行することである。さらに、ワークフローが書き込み権限を持ち、信頼できない公開の入力を受け取る場合、リスクは通常スキルそのものではなく、スキルを取り巻くトリガーの設計、入力の扱い、実行時の権限にあると付け加えている。

## 採用とエコシステム

メンテナーたちの助言は、ワークフローがローカルで安定してから初めて CI に移すことである。なぜなら、手作業で使う段階こそが、指示をデバッグし、スクリプトを洗練し、現実のエッジケースを見つける場だからである。この Action は、GitHub 上での Codex による自動 PR レビューとは別物であり、同じ記事は後者をリポジトリのスループットに寄与する別の要素として扱っている。
