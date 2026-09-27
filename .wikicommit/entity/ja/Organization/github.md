---
title: "GitHub"
type: "schema:Organization"
lang: ja
tags: [コーディングツール, エージェント]
translated_from: ".wikicommit/entity/en/Organization/github.md"
source_commit: "a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Git ホスティング、プルリクエスト、Actions を支える開発者プラットフォームであり、GitHub Copilot とそのコーディングエージェントの提供元。"
  url: "https://github.com/"
---

GitHub は、Git ホスティング、プルリクエスト、GitHub Actions といった基本的な仕組みを提供する開発者プラットフォームであり、これらの仕組みはこの wiki で扱う多くのツールの土台となっている。また、[[SoftwareApplication/github-copilot]] と [[SoftwareApplication/github-copilot-coding-agent]] の提供元でもある。GitHub は自らの歴史を振り返る中で、ソフトウェアの作られ方に潜む構造的な問題に繰り返し取り組んできたと説明している。すなわち、Git を誰でも使えるものにし、プルリクエストによってコードレビューを体系化し、Actions によってデプロイを自動化してきた、というものである。

Universe 2025 での発表時点で、GitHub はプラットフォーム上の開発者数が 1 億 8,000 万人に達したと報告し、過去最速のペースで成長していると述べた。毎秒 1 人の新しい開発者が加わり、新規開発者の 80% が最初の 1 週間で Copilot を使っているという。これらはプロダクト発表の中で公表された GitHub 自身の数字である。

## 活動・製品

GitHub のエージェント型プロダクトは、プラットフォームの基本的な仕組みと並立するのではなく、その上に構築されている。[[SoftwareApplication/github-copilot-coding-agent]] は GitHub Actions 上で動作し、成果をドラフトのプルリクエストとして提出する。[[SoftwareApplication/agent-hq]] は同じ流れを他社のコーディングエージェントにも広げつつ、Git、プルリクエスト、Issue、Actions を作業の場として維持している。GitHub は 2018 年に導入した Actions を世界最大の CI/CD エコシステムと位置づけており、GitHub Marketplace には 25,000 を超えるアクションがあり、GitHub ホステッドランナーとセルフホステッドランナーを合わせて毎日 4,000 万件を超えるジョブが実行されていると説明している。
