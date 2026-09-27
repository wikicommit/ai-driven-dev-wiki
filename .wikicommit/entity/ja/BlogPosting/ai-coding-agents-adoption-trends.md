---
title: "AI コーディングエージェント：導入の動向"
type: "schema:BlogPosting"
lang: ja
tags: [コーディングツール, 導入, 開発者調査]
translated_from: ".wikicommit/entity/en/BlogPosting/ai-coding-agents-adoption-trends.md"
source_commit: "35d96aaa33f4f9b2ab6d25c70a59d6ec1d1c503a"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "1 万 5,000 人を超えるプロのソフトウェア開発者を対象とした Developer Ecosystem Survey 2026 に基づき、職場での AI コーディングツールの導入状況を報告する JetBrains Research の記事。2026 年 5〜7 月の数値では、Claude Code が最も広く使われるツールとなり、GitHub Copilot と Cursor は減少している。"
  author: ["Mikhail Bogdanov"]
  publisher: "JetBrains"
---

JetBrains Research ブログのこの記事は、プロの開発者が職場で AI コーディングエージェントをどのように使っていたかを、JetBrains の Developer Ecosystem Survey 2026 に基づいて報告している。この調査は、1 万 5,000 人を超えるプロの開発者を対象とした、大規模で世界全体を代表する調査の第 10 回と説明されている。見出しとなる数値は、2026 年 5〜7 月時点で、プロの開発者の 90% がローカルかリモートかを問わず AI コーディングエージェントを職場で少なくとも週 1 回使っており、68% が毎日使っていたというものである。

記事の大部分は、個々のツールを職場での導入率と認知度で比較し、2026 年 5〜7 月の数値をそれ以前の数値と比べている。比較対象はおもに 2026 年 1 月の数値で、GitHub Copilot については 1 年前の数値である。中心的な発見は、[[SoftwareApplication/claude-code]] が職場で最も広く導入された AI コーディングツールへと躍進したことであり、あわせて [[SoftwareApplication/openai-codex]] の急成長と、[[SoftwareApplication/github-copilot]] と [[SoftwareApplication/cursor]] の減少が示されている。記事は最後に、JetBrains 自身のエージェント製品と統合について説明して締めくくっている。

## 要点

- 2026 年 5〜7 月時点で、調査対象のプロの開発者の 90% が職場で AI コーディングエージェントを少なくとも週 1 回使い、68% が毎日使っていた。
- 世界のプロの開発者のおよそ 39% が職場で Claude Code を使っており、2026 年 1 月の 18% から増加した（米国では 47%）。記事は、Claude Code は GitHub Copilot の 2 倍の頻度で使われており、31% の開発者にとって最もよく使う AI コーディングツールになっていると述べ、これを日常的な利用から単独で最もよく使うツールへの約 80% の転換率と呼んでいる。
- Codex の職場での導入率は 2026 年 1 月の 3% から 16% へとおよそ 5 倍に伸び、認知度は開発者の 27% から 65% に上昇した。
- GitHub Copilot の導入率は 1 年前の 29% から 21% に低下したが、認知度は 79% と、依然として最もよく知られたツールの 1 つであった。
- Cursor の認知度は 69% から 75% に上昇した一方、導入率は 18% から 12% に低下し、最大の落ち込みは中国で報告された（28% から 16%）。
- オープンソースのコーディングエージェントである [[SoftwareApplication/opencode]] は、導入率 7%、認知度 42% に達した。記事は、大企業の後ろ盾がないツールとしては注目に値するとしている。
- [[SoftwareApplication/google-antigravity]] は導入率 6% で横ばいだったが、認知度は 29% から 47% に上昇した。最も強い市場はインドで、導入率は 15% だった。
- JetBrains は、開発者のおよそ 9% が職場で同社の IDE に組み込まれた AI や同社の Junie エージェント（あるいはその両方）を使っていると報告している。

## 背景

これらの数値は、開発ツールのベンダーが公表した自己申告の調査データであり、記事の最後の部分は JetBrains 自身の製品、すなわち Agent Client Protocol を介した同社 IDE へのエージェント統合、プレビュー版のエージェント型開発環境 Air、そして JetBrains Central を宣伝している。方法論の注記によれば、「プロの開発者」にはコーディングに関連するいくつかの職種の回答者が含まれ、その約 90% は開発者、プログラマー、またはソフトウェアエンジニアである。また、調査は 8 言語にローカライズされ、地域ごとの回答割り当てが設けられており、結果は地域、雇用形態、プログラミング言語、JetBrains 製品への習熟度によって統計的に再重み付けされている。
