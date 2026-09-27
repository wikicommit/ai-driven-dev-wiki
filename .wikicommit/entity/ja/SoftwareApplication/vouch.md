---
title: "Vouch"
type: "schema:SoftwareApplication"
lang: ja
tags: [オープンソース, メンテナー, 信頼]
translated_from: ".wikicommit/entity/en/SoftwareApplication/vouch.md"
source_commit: "fc6f8839ef49b4ad99a056d9f2d3011a9e22d960"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Mitchell Hashimoto による実験的なオープンソースプロジェクト。オープンソースへの貢献に明示的な信頼管理を導入するもので、コントリビューターは参加する前に、信頼されたメンテナーから保証（vouch）を受けなければならない。"
---

Vouch は、GitHub 上でホストされている Mitchell Hashimoto によるプロジェクトで、オープンソースプロジェクト向けの明示的な信頼管理の仕組みを実装している。この仕組みでは、コントリビューターは参加する前に、信頼されたメンテナーから保証（vouch）を受けなければならない。GitHub の Director of Open Source Programs は、[[BlogPosting/welcome-to-the-eternal-september-of-open-source]] の中でこれを、オープンソースの [[DefinedTerm/eternal-september]] と表現される、手間をかけていない貢献の殺到に対して、コミュニティが独自の対応策を築いている興味深い例として挙げている。その一方で、Vouch が実験的なものであり、その一部の側面には議論の余地があるだろうとも述べている。

## 導入とエコシステム

記事は Vouch を、オープンソースにおける信頼の仕組みの長い系譜 ― Advogato の信頼メトリクス、Drupal のクレジットシステム、Linux カーネルの `Signed-off-by` チェーン ― の中に位置づけ、招待制のワークフローや、コントリビューターのトリアージと評判スコアリングのための独自の GitHub Actions といった、他のコミュニティによる取り組みと並べて紹介している。
