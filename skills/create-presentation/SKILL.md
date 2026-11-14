---
name: create-presentation
description: >-
  Guides the agent to create, structure, design, or convert presentation slide notes
  optimized for the Obsidian Presenter plugin. Use this skill whenever the user wants to
  create a presentation, write slides in Markdown, convert notes/documents into a slide deck,
  design consulting-grade proposal or reporting slides, or format presentation content with
  action titles, multi-columns, business frameworks (pyramid, funnel, 2x2 matrix, cycle),
  bar charts, Bento grids, KPIs, badges, and speaker notes.
license: MIT
---

# Create Presentation Skill

Obsidian Presenter プラグイン（`markdown-presenter` v1.6.1+）の仕様とコンサルティングファーム基準のスライド設計原則に準拠したプレゼンテーション資料（Markdownノート）を作成・構造化・変換するためのガイドラインです。

詳細な記法は [references/syntax-guide.md](./references/syntax-guide.md)、全13種のテンプレートと具体例は [references/design-patterns.md](./references/design-patterns.md) を参照してください。

---

## ワークフロー (Workflow)

```text
[Phase 1: 要件・目的の整理]
       ↓
[Phase 2: ストーリーライン (SCQA) & スライド構成の設計]
       ↓
[Phase 3: スライド執筆 (アクションタイトル & Presenter記法)]
       ↓
[Phase 4: デザイン6原則・はみ出し防止 & 発表者ノート推敲]
       ↓
[Phase 5: プレビュー・エクスポート案内]
```

---

### Phase 1: 要件・目的の整理

ユーザーの入力が「新規作成」か「既存ドキュメントの変換」かを判断し、以下を整理します。

1. **種別・目的**: 企画・事業提案 / 経営報告 / 技術発表・LT / 定例・進捗報告
2. **オーディエンス**: 経営陣・決裁者 / クライアント / エンジニア / 非エンジニア全般
3. **発表時間・想定枚数**: 5分LT（5〜8枚） / 15〜30分（10〜20枚）
4. **配色（70:25:5の法則）**: ベース（背景 70%）、メイン（文字・見出し 25%）、アクセント（強調 5%）

#### 対話分岐と出力先のルール
- **即生成の原則**: 既存メモ・ドキュメントの変換や、目的・対象がある程度読み取れる指示では、不足項目を合理的に仮定して**質問で止めずにまず初稿を生成**し、末尾で微調整の要否を確認します。
- **事前確認**: テーマが抽象的すぎる場合（例：「提案スライドを作りたい」のみ）に限り、上記1〜3を2〜3問で簡潔に確認します。
- **出力先と上書き防止**: 既存ノートをスライド化する場合、元のノートを上書き破壊しないよう別ファイル（例: `*-slides.md`）への作成またはチャット上への提示を基本とし、明示的な指示がある場合のみ元ファイルを更新します。

> [!TIP]
> 既存のメモや議事録が与えられた場合は、単なる転記ではなく「結論ファースト（ピラミッド原則）」で要約・再構造化します。

---

### Phase 2: ストーリーライン (SCQA) & スライド構成の設計

本文を書く前に、全体の論理構成と各スライドのレイアウト型を設計します。

1. **SCQAフレームワークによる導入設計**:
   - **S (Situation)**: 誰もが同意する現状・背景
   - **C (Complication)**: そこに生じた変化・放置できない課題・ボトルネック
   - **Q (Question)**: 解決すべき中心的な問い
   - **A (Answer)**: 提案する結論・ソリューション（エグゼクティブサマリー）
2. **シンプルで伝わるアクションタイトル（1行・25文字前後）**:
   - 各スライドの `## H2` は単なる名詞ラベル（例: `× 売上推移`）ではなく結論を伝える表現にしつつ、**20〜28文字以内（1行に収まる長さ）** に凝縮します。
   - 「〜により」「〜を踏まえて」等の冗長な修飾語を削ぎ落とし、**「対象 ＋ 結論（動詞・数値）」** の端的なフレーズにします（例: `◯ クラウドAIが+140%成長し増収の65%を牽引`）。
   - 背景や補足理由はタイトルに詰め込まず、直下の `> [!important]` や本文・`> [!note]` に逃がします。
   - **中扉（`section`）**: さらに短い **10〜15文字程度の名詞句**（例: `01. 現状の課題`）にします。
   - **検証基準**: 本文を見ずに `## H2` だけを順に読んでもストーリーが通じること。
3. **伝達目的に応じたレイアウト選定**:
   - 表紙（`# H1`）、中扉（`## 見出し` のみ）、ビッグステートメント（`> ...` のみ）を適宜挟み、単調な箇条書きの連続を避けます。
   - 構造化・データ提示には [design-patterns.md](./references/design-patterns.md) の「伝達目的から選ぶ最適レイアウト早見表（全13型）」から最適なパターンを選択します（エグゼクティブサマリー、ステップフロー、2カラム対比、3カラム、2軸マトリクス、ピラミッド、ファネル、サイクル、スイムレーン、チャート＋インサイト、KPIビッグナンバー、Bentoグリッド）。

---

### Phase 3: スライド執筆 (Presenter記法の適用)

構文・ディレクティブの正確な書式と具体例は [references/syntax-guide.md](./references/syntax-guide.md) に従います。執筆時の判断基準は以下の通りです。

1. **フロントマター（ゼロ設定の原則）**:
   - 基本設定はプラグイン設定が適用されるため、上書きしたい項目のみ最小限記述します（0行でも動作）。
   - レイアウト崩れ防止のため `fit: auto` の付与を推奨します。
   ```yaml
   ---
   header: "2026年度 提案資料"
   accentColor: "#2563eb"
   fit: auto
   ---
   ```
2. **見出し階層と改スライド**:
   - `# H1`: 表紙（中央配置） / `## H2`: スライドタイトル（自動改スライド） / `### H3`: スライド内・カラム見出し（改スライドしない）。
   - `---`（空行挟み）で分割した場合、親 `## H2` が自動継承され `タイトル 1-1`, `1-2` と連番が付与されます（無効化は `inheritHeadings: false`）。
3. **マルチカラム & 図解ディレクティブの使い分け**:
   - 比較・解説: `<!-- columns 2 1:2 card -->`（左テキスト・右図表）または `<!-- columns 2 2:1 card -->`（左チャート・右インサイト）。
   - 並列・手順: `<!-- columns 3 card -->` または `<!-- columns 3 step -->`。
   - フレームワーク: `<!-- columns pyramid -->` / `funnel` / `matrix`（右上を最優先 `🎯` に配置） / `cycle`（記述順に注意）。
   - 定量グラフ: `<!-- chart --> ... <!-- /chart -->`（`- ラベル | 値 | %` 形式）。
4. **視覚的装飾と強調ルール（使いすぎ注意：5%の原則）**:
   - バッジ（`[重要]`, `[課題]`, `[ボトルネック]`, `[最優先]`, `[決裁]`, `[牽引]` など）や `🎯` を含めると、該当カラム・図解行が自動的にアクセント強調されます。
   - 単一数値の強調には単独行太字（`**+140%**`）または `<!-- kpi -->`、結論強調には `> [!important]` / `> [!tip]` / `> [!warning]` を使用します。
5. **エクスポート互換性と図解表現**:
   - **独自HTMLタグの禁止**: `.pptx` エクスポート時の再現性崩壊を防ぐため、素の `<div>` や `<span>` 等は使わず、標準Markdown＋Presenter公式ディレクティブのみで構成します。
   - **Mermaid・画像活用**: 技術構成・シーケンス・フローの説明には、テキストの羅列ではなく ```` ```mermaid ```` や Vault 内画像（`![[...]]`）を積極活用します。

---

### Phase 4: デザイン6原則・はみ出し防止 & 発表者ノート推敲

1. **チェックリスト**:
   - **タイトルの簡潔さ**: `## H2` が20〜28文字以内（1行）で端的に結論を伝えているか？（中扉は10〜15文字程度）
   - **1スライド・1メッセージ**: 3〜5秒でスキャンできる情報量か（目安：箇条書き3〜5行、日本語100字程度）。
   - **はみ出し回避**: 詰め込まず、`---` で分割するか詳細を `> [!note]` へ逃がす。テーブルは原則 **3〜4列以内** とし、セル内は簡潔な語句に抑える。
   - **整列の原則**: 並列カラム（`columns 2` / `3`）の各列で見出し長・行数・粒度を揃える。
   - **視線誘導**: 2カラム時は「左に主張、右に証拠」または「左にチャート、右にインサイト」を一貫させる。
2. **発表者ノート 兼 詳細解説 (`> [!note]`)**:
   - 背景説明、補足データ、口頭トークスクリプトは `> [!note]` に分離します（プレゼン本番では `N` キーで開閉、単一HTML配布資料モード・PDFハンドアウトでは詳細解説として展開、PPTXではネイティブの発表者ノートに格納されます）。

---

### Phase 5: プレビュー・エクスポート案内

スライド提示後、必要に応じて以下の操作を簡潔に案内します。

- **プレビュー・はみ出し確認**: エディタ右上の **TVアイコン**（`Presenter: Open slide preview`）でリアルタイム確認、ツールバーの `⚠`（`Presenter: Check slide overflow`）ではみ出し検査が可能。
- **テンプレート追記**: コマンドパレットの `Presenter: Insert slide template (quick picker)...` またはプレビュー上部のテンプレートアイコン（`Presenter: Insert slide template...`）から追加可能。
- **プレゼン開始・配布出力**: プロジェクターアイコン（`Presenter: Start presentation`）で投影、`Presenter: Export presentation as standalone HTML`（目次付き配布HTML）や `Presenter: Export presentation as powerpoint (.pptx)`（編集可能PPTX）でエクスポート可能。

---

## リファレンス & テンプレート

- **記法・ディレクティブ完全リファレンス**: [references/syntax-guide.md](./references/syntax-guide.md)
- **コンサルティング・デザインパターン集 (全13型＋6原則)**: [references/design-patterns.md](./references/design-patterns.md)
- **テンプレート**:
  - [ビジネス提案・企画書テンプレート](./resources/templates/business-proposal.md)
  - [技術発表・LTテンプレート](./resources/templates/tech-talk.md)
  - [プロジェクト進捗・定例報告テンプレート](./resources/templates/project-report.md)
