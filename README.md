# Obsidian Presenter - AI Slide Authoring Skill (`create-presentation`)

[Obsidian Presenter](https://github.com/xhisashix/obsidian-plugin-presenter) プラグインに完全最適化されたプレゼンテーション用Markdownスライドを作成・構造化・変換するための AI エージェントスキル（Agent Skill）です。

Google Antigravity や Claude Code などのエージェントツールと連携し、自然言語のプロンプトから直感的に美しいスライド資料を作成できます。

---

## 主な特徴 (Features)

- **Obsidian Presenter 最新記法への完全準拠 (v1.6+ 対応)**:
  - `# H1`: 表紙スライド（タイトル・サブタイトル・中央揃え）
  - `## H2`: 各スライドのアクションタイトル（自動改スライド・`---` 分割時の見出し自動継承 `1-1, 1-2` 対応）
  - `### H3`: カラム内見出し・サブセクション・図解の各ティア見出し
- **コンサルティング・スライドの6大原則 & 全13種のフレームワーク構築**:
  - SCQAストーリー設計とアクションタイトル（結論ファーストの完全文）の徹底
  - **ビジネスフレームワーク図解**: ピラミッド階層図（`<!-- columns pyramid -->`）、ファネル分析図（`<!-- columns funnel -->`）、2軸4象限マトリクス（`<!-- columns matrix -->`）、循環サイクル図（`<!-- columns cycle -->`）
  - **定量データ＆チャート**: 水平バーチャート（`<!-- chart -->`）、KPIビッグナンバー（`<!-- kpi -->` または `**+140%**`）、弁当箱型ダッシュボード（Bento Box）、エグゼクティブサマリー（Situation / Findings / Recommendation）
- **マルチカラム・レイアウト**:
  - `<!-- columns 2 card -->` や `<!-- columns 2 plain -->` によるカード／プレーン分割
  - `<!-- columns 2:1 -->` / `<!-- columns 1:2 -->` / `<!-- columns 3:1 -->`（図表＋解説）や `<!-- columns 3 step -->`（手順・プロセスの可視化）
- **スマートレイアウト & 視覚的ハイライト**:
  - 中扉スライド（`section`）やビッグステートメント引用（`quote`）の自動適用
  - `[重要]`, `[課題]`, `[ボトルネック]`, `[最優先]`, `[決裁]`, `[牽引]` などの自動装飾バッジ
  - `🎯` や重要バッジを含むカラム・図解ティアの自動強調枠表示（`.presenter-col-highlight`）
  - `> [!important]` などの Obsidian Callout による結論サマリー
- **発表者ノート & マルチフォーマット配布対応 (HTML / PPTX / PDF)**:
  - `> [!note]` を活用し、プレゼン本番の大画面には要点だけを表示、発表者には手元カンペ（`N` キー）を提供
  - **単一HTMLエクスポート**: 階層目次（TOC）サイドバー付き配布資料モードや全スライド一覧グリッド（`G` キー）で詳細解説を展開
  - **PowerPoint (`.pptx`) エクスポート**: 編集可能なネイティブシェイプ・表・スピーカーノートとして出力
  - **ハンドアウト印刷 (PDF)**: A4 1ページにスライド＋詳細解説が並ぶ SlideDoc 形式で出力
- **スライドはみ出し（Overflow）防止**:
  - 1スライド1メッセージ・整列の原則の徹底、`fit: auto`（自動縮小フィット）の付与

---

## ディレクトリ構成

```text
skills/
└── create-presentation/
    ├── SKILL.md                  # スキルメイン定義（ワークフロー・推敲・手順）
    ├── references/
    │   ├── syntax-guide.md       # Presenter記法完全リファレンス
    │   └── design-patterns.md    # 定番デザインパターン集（比較、ステップ、KPI等）
    └── resources/
        └── templates/
            ├── business-proposal.md  # 企画・提案書テンプレート
            ├── tech-talk.md          # 技術勉強会・LTテンプレート
            └── project-report.md     # プロジェクト進捗・定例報告テンプレート
```

---

## インストール方法 (Installation)

### 方法 1: GitHub CLI (`gh skill`) でインストールする場合（推奨）

GitHub CLI (`gh` v2.90.0 以降) を使用して、1コマンドで直接インストールできます。

```bash
# Obsidian Vault のルートディレクトリへ移動
cd /path/to/your-obsidian-vault

# 現在のプロジェクト（.agents/skills）にインストール
gh skill install xhisashix/obsidian-presenter-skill

# 特定のエージェント（Claude Code 等）を指定する場合
gh skill install xhisashix/obsidian-presenter-skill --agent claude-code

# マシン全体（グローバル）で使えるようにインストールする場合
gh skill install xhisashix/obsidian-presenter-skill --scope user
```

### 方法 2: 手動で配置する場合

#### A. 特定の Obsidian Vault で使う場合

お使いの Obsidian Vault のルートディレクトリで、リポジトリのスキルフォルダを配置します。

```bash
cd /path/to/your-obsidian-vault

# git clone して必要なスキルをコピー
git clone https://github.com/xhisashix/obsidian-presenter-skill.git /tmp/presenter-skill
mkdir -p .agents/skills
cp -R /tmp/presenter-skill/skills/create-presentation .agents/skills/
rm -rf /tmp/presenter-skill
```

#### B. マシン全体（グローバル）で使う場合 (Antigravity)

すべてのワークスペースで利用可能にする場合は、グローバル設定ディレクトリに配置します。

```bash
mkdir -p ~/.gemini/config/skills
git clone https://github.com/xhisashix/obsidian-presenter-skill.git /tmp/presenter-skill
cp -R /tmp/presenter-skill/skills/create-presentation ~/.gemini/config/skills/
rm -rf /tmp/presenter-skill
```

---

## 使い方 (Usage)

スキルを配置後、AIアシスタントに自然言語で指示するだけで自動的に呼び出されます。

### プロンプト例

- **新規企画スライドの作成**:
  > 「来期の新規AIサービス導入に関する提案スライドを作成して。経営陣向けに、現状課題、ソリューション、ロードマップ、期待されるROI（工数削減など）を盛り込んで。」
- **既存ドキュメントのスライド化**:
  > 「このノート（または議事録）の内容を、Obsidian Presenterで発表できるスライド形式に要約・構造化して。」
- **技術LTスライドの作成**:
  > 「5分間の社内LT用に、Obsidian Presenterの魅力を伝えるスライドをコード例付きで作成して。」

---

## 関連リポジトリ

- **[Obsidian Presenter Plugin](https://github.com/xhisashix/obsidian-plugin-presenter)**:
  本スキルで生成したMarkdownスライドをObsidian上で美しくプレビュー・プレゼン・エクスポートするためのプラグイン本体。

---

## ライセンス

MIT License
