---
title: "Vibe Kanban"
type: "schema:SoftwareApplication"
lang: ja
tags: [マルチエージェント, オーケストレーション, エージェンティックコーディング, git worktree]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/vibe-kanban.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "並行するコーディングエージェントを調整するためのクロスプラットフォームのカンバンボード。各タスクカードが専用の git worktree とブランチを持ち、diff はボード内でレビューされ、実行中のエージェントへフィードバックが送られる。"
  applicationCategory: "DeveloperApplication"
  author: ""
  operatingSystem: "macOS, Windows, Linux"
  softwareVersion: ""
  license: ""
---

Vibe Kanban は、並行するコーディングエージェントの作業をカンバンボードとして整理する、クロスプラットフォームのローカルオーケストレータである。タスクカードは詳細なプロンプトを担い、カードを "In Progress" へドラッグすると、そのタスクに専用の git worktree とブランチが与えられる。diff はボードの内側でレビューされ、エージェントがまだ実行中のあいだにフィードバックが送られる。

## 概要

[[BlogPosting/the-code-agent-orchestra]] はこれをそのツールの情勢の Tier 2——ローカルオーケストレータ——に置き、狙う具体的な問題を「doomscrolling gap」——エージェントが作業していて開発者にやることがない2〜5分——だと記述する。並行する作業の待ち行列をボードとして可視化することが、その手持ち無沙汰な時間に対して差し出される答えである。

## 機能

詳細なプロンプトを備えたタスクカード、タスクごとの worktree とブランチ、ボード内での diff のレビュー、そして実行中のエージェントへフィードバックを送る機能。[[SoftwareApplication/claude-code]]、[[SoftwareApplication/codex]]、[[SoftwareApplication/gemini-cli]]、Amp、[[SoftwareApplication/cursor]] Agent CLI などに対応する。

## 沿革

ここで参照できる説明は、これが Mac、Windows、Linux で動作し、無償であり、鍵は自分で用意する方式であることを述べている。
