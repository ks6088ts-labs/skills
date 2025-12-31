# skills

AI エージェント向けのスキル集です。

## Agent Skills 一覧

| スキル名 | 説明 | トリガー例 |
|---------|------|-----------|
| [agents-md-creator](skills/agents-md-creator/SKILL.md) | AIコーディングエージェント向けの指示書「AGENTS.md」を作成するスキル | 「AGENTS.mdを作成」「AIエージェント用の指示書を作る」「エージェント向けREADMEを作成」 |
| [architecture-design-creator](skills/architecture-design-creator/SKILL.md) | PRDと機能設計書に基づいてアーキテクチャ設計書を作成するスキル | 「アーキテクチャ設計書を作成して」「技術仕様書を書いて」「architecture design を作って」 |
| [code-review](skills/code-review/SKILL.md) | コードの品質、セキュリティ、テスト、パフォーマンス、アーキテクチャの観点から包括的なコードレビューを実施するスキル | 「コードレビュー」「コードをチェック」「PRをレビュー」「このコードを確認して」 |
| [doc-review](skills/doc-review/SKILL.md) | 提案書、設計書、PRD、技術仕様書などのドキュメントを多角的にレビューするスキル | 「ドキュメントをレビュー」「提案書をチェック」「設計書を確認」「この文書をレビューして」 |
| [doc-writer](skills/doc-writer/SKILL.md) | PRDに基づいてドキュメント執筆を支援するスキル | 「ドキュメントを書く」「仕様書を作成」「ガイドを作る」 |
| [functional-design-creator](skills/functional-design-creator/SKILL.md) | PRDに基づいて機能設計書を作成するスキル | 「機能設計書を作成して」「PRDから設計書を作って」「functional design を書いて」 |
| [glossary-creator](skills/glossary-creator/SKILL.md) | プロジェクト固有の用語と技術用語を体系的に定義する用語集を作成するスキル | 「用語集を作成して」「glossary を作って」「用語を定義して」 |
| [prd-creator](skills/prd-creator/SKILL.md) | プロダクト要求仕様書（PRD）を作成するスキル | 「PRDを作成」「プロダクト要求仕様書を書いて」「要件定義を作成」 |
| [press-release-creator](skills/press-release-creator/SKILL.md) | Amazon の Working Backwards 手法に基づいたプレスリリース＋FAQを作成するスキル | 「プレスリリースを作成」「PR/FAQ を書いて」「Working Backwards で企画」 |
| [skill-creator](skills/skill-creator/SKILL.md) | 効果的なスキルを作成するためのガイドを提供するスキル | 「スキルを作成」「新しいスキルを作って」「スキルを更新」 |

## スキルの分類

### ドキュメント作成系

| スキル名 | 出力先 | 前提条件 |
|---------|--------|----------|
| prd-creator | `docs/prd.md` | なし |
| functional-design-creator | `docs/functional-design.md` | `docs/prd.md` |
| architecture-design-creator | `docs/architecture.md` | `docs/prd.md`, `docs/functional-design.md` |
| glossary-creator | `docs/glossary.md` | なし（PRD等があると効果的） |
| press-release-creator | `docs/press-release.md` | なし |
| doc-writer | 各種ドキュメント | `docs/prd.md` |
| agents-md-creator | `AGENTS.md` | なし |

### レビュー系

| スキル名 | 対象 | 主な観点 |
|---------|------|----------|
| code-review | ソースコード | セキュリティ、正確性、コード品質、テスト、パフォーマンス |
| doc-review | ドキュメント全般 | 戦略・ビジネス、論理構造、技術的妥当性、リスク管理 |

### メタスキル

| スキル名 | 用途 |
|---------|------|
| skill-creator | 新しいスキルの作成・更新