---
name: create-presentation
description: >-
  Guides the agent to create, structure, design, or convert presentation slide notes
  optimized for the Obsidian Presenter plugin. Use this skill whenever the user wants to
  create a presentation, write slides in Markdown, convert notes/documents into a slide deck,
  design proposal or reporting slides, or format presentation content with multi-columns,
  KPIs, badges, and speaker notes.
---

# Create Presentation Skill

このスキルは、Obsidian Presenter プラグイン（`markdown-presenter`）の仕様・記法に完全準拠した美しいプレゼンテーション資料（Markdownノート）を作成・構造化・変換するためのガイドラインです。

---

## ワークフロー (Workflow)

```
[Phase 1: 要件・目的の整理]
       ↓
[Phase 2: ストーリーライン & スライド構成の設計]
       ↓
[Phase 3: スライド執筆 (Presenter記法準拠)]
       ↓
[Phase 4: はみ出し防止 & 発表者ノート推敲]
       ↓
[Phase 5: プレビュー・プレゼン・エクスポート案内]
```

---

### Phase 1: 要件・目的の整理

ユーザーの入力内容に応じて、新規作成か既存ドキュメントの変換かを判断し、以下の前提を確認します。

1. **プレゼンテーションの種別・目的**:
   - 企画書・事業提案（課題解決、ROI、ロードマップ）
   - 技術発表・勉強会・LT（コード例、アーキテクチャ図、Tips）
   - 定例・進捗報告（KPI、進捗ステータス、課題と対策）
   - その他一般的なプレゼンテーション
2. **ターゲット読者 / オーディエンス**:
   - 経営陣 / クライアント / エンジニア / 非エンジニア全般
3. **発表時間・想定スライド枚数**:
   - 5分LT（5〜8枚程度） / 15分〜30分（10〜20枚程度）
4. **デザインテーマ・アクセントカラー**:
   - コーポレートカラーや発表内容に合った色（例: 青 `#2563eb`, 緑 `#10b981`, 橙 `#f59e0b`, 赤 `#e11d48`）

> [!TIP]
> 既存のメモや文章が与えられている場合は、内容を要約・抽出しながらスライド化を進めます。

---

### Phase 2: ストーリーライン & スライド構成の設計

いきなり本文を書く前に、全体の流れ（ストーリー）を組み立てます。

- **表紙 (Cover)**: 魅力的なタイトル、サブタイトル、発表者名、日付
- **アジェンダ / 目次**: `<!-- columns 3 step card -->` などを活用した3〜4パート構成
- **各パートの中扉 (Section)**: 見出しのみのシンプルなスライド（Smart Layoutsで中央巨大表示）
- **本文スライド (Content)**:
  - 1スライド = 原則1メッセージ
  - 課題と解決策の対比（2カラム）
  - 図・表と要点解説（2:1カラム）
  - 定量実績の強調（KPIビッグナンバー）
- **まとめ & 次のアクション**: キーテイクアウェイ、Calloutによる強い結論

---

### Phase 3: スライド執筆 (Presenter記法の適用)

Obsidian Presenter の仕様に従ってMarkdownを作成します。詳細な記法リファレンスは [references/syntax-guide.md](./references/syntax-guide.md) および [references/design-patterns.md](./references/design-patterns.md) を参照してください。

#### 1. フロントマター（ゼロ設定の原則）
- 基本設定はObsidianの設定値が適用されるため、**上書きしたい項目のみを最小限**記述します。
- レイアウト崩れを防ぐため、`fit: auto`（はみ出し自動縮小）を付与することを推奨します。

```markdown
---
header: "2026年度 提案資料"
accentColor: "#2563eb"
fit: auto
---
```

#### 2. 見出し階層ルール
- `# H1`: プレゼン全体の「表紙」スライド（中央配置）
- `## H2`: 各スライドの「タイトル」（自動的に改スライド）
- `### H3`: スライド内の小見出し、またはカラム内の見出し（改スライドしない）
- `---`: 空行で挟むことで、H2以外の任意の箇所で明示的にスライド分割

#### 3. マルチカラムの活用
- **2カラム比較**:
  ```markdown
  <!-- columns 2 card -->
  ### 課題
  - 箇条書き...
  ### 解決策
  - 箇条書き...
  <!-- /columns -->
  ```
- **3ステップ手順**:
  ```markdown
  <!-- columns 3 step card -->
  ### ステップ 1
  内容...
  ### ステップ 2
  内容...
  ### ステップ 3
  内容...
  <!-- /columns -->
  ```
- **図表＋解説 (2:1 比率 & プレーンスタイル)**:
  ```markdown
  <!-- columns 2:1 plain -->
  ### システム構成図
  ```mermaid
  flowchart LR
    A --> B
  ```
  ### 設計のポイント
  - ポイント1
  - ポイント2
  <!-- /columns -->
  ```

#### 4. 視覚的装飾 (Badges & KPIs & Callouts)
- **バッジ**: `[重要]`, `[課題]`, `[POINT]`, `[STEP 1]` と書くだけでアクセントカラーのバッジに装飾。
- **KPIビッグナンバー**: 単独行の太字数値（例: `**+140%**`, `**3.5x**`, `**-65%**`）は自動で巨大フォント化。
- **結論ボックス**: `> [!important] Key Takeaway` でスライドの最重要メッセージを強調。

---

### Phase 4: はみ出し防止 & 発表者ノート推敲

1. **はみ出し（Overflow）の防止**:
   - スライド1枚あたりの文字数は**箇条書き3〜5行**を目安とします。
   - スライド内に長文の段落をベタ書きしないようにします。
2. **発表者ノート 兼 詳細解説 (`> [!note]`) の活用**:
   - スライド上は要点のみを簡潔にまとめ、背景説明、補足データ、発表時のトークスクリプトは `> [!note]` に記述します。
   - **メリット**:
     - 投影時は大画面から自動的に隠れ、手元カンペ（`N` キー）になります。
     - 単一HTMLエクスポートやハンドアウト印刷時には「スライド ＋ 詳細解説」として綺麗に展開されるため、非エンジニアへの配布資料としても完璧に機能します。

---

### Phase 5: プレビュー・操作・配布の案内

スライドMarkdownを提示した後、ユーザーに対して以下の利用手順・Tipsを添えて案内します。

1. **プレビューの確認**:
   - エディタ右上の **「TV」アイコン** または `Presenter: Open slide preview` コマンドでエディタ横にリアルタイムプレビューを開く。
2. **プレゼンテーション本番**:
   - 左リボンのプロジェクターアイコン、またはプレビュー上部の「開始」ボタンで全画面プレゼンを開始。
   - **操作ショートカット**:
     - `Space` / `→` : 次のスライド
     - `N` : 発表者ノートの開閉
     - `G` / `O` : 全スライド一覧グリッド（Q&Aジャンプ用）
     - `画像クリック` : 画像やMermaid図のLightbox拡大
3. **資料配布・エクスポート**:
   - **ブラウザ閲覧用**: コマンド `Presenter: Export presentation as standalone HTML` でObsidian不要の単一HTMLを出力。
   - **PDF / 印刷**: ツールバーの印刷ボタンから「Print handout with notes（スライド＋解説）」または「Print slides only」を選択してPDF保存。

---

## テンプレート参照 (Templates)

目的に応じて以下のテンプレートを活用してください：

- [ビジネス提案・企画書テンプレート](./resources/templates/business-proposal.md)
- [技術発表・LTテンプレート](./resources/templates/tech-talk.md)
- [プロジェクト進捗・定例報告テンプレート](./resources/templates/project-report.md)
