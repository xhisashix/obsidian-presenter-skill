# Obsidian Presenter - AI Slide Authoring Skill (`create-presentation`)

[Obsidian Presenter](https://github.com/xhisashix/obsidian-plugin-presenter) プラグインに完全最適化されたプレゼンテーション用Markdownスライドを作成・構造化・変換するための AI エージェントスキル（Agent Skill）です。

Google Antigravity や Claude Code などのエージェントツールと連携し、自然言語のプロンプトから直感的に美しいスライド資料を作成できます。

---

## 主な特徴 (Features)

- **Obsidian Presenter 記法への完全準拠**:
  - `# H1`: 表紙スライド（タイトル・サブタイトル・中央揃え）
  - `## H2`: 各スライドのタイトル（自動スライド区切り）
  - `### H3`: カラム内見出し・サブセクション
- **マルチカラム・レイアウト**:
  - `<!-- columns 2 card -->` や `<!-- columns 2 plain -->` によるカード／プレーン分割
  - `<!-- columns 2:1 plain -->`（図表＋解説）や `<!-- columns 3 step card -->`（手順・プロセスの可視化）
- **スマートレイアウトの自動活用**:
  - 中扉スライド（見出しのみのスライドを自動中央巨大表示）
  - ビッグステートメント（引用 `> ...` のスタイリッシュな強調）
- **視覚的装飾**:
  - `[重要]`, `[課題]`, `[STEP 1]` などの自動装飾バッジ
  - 単独行の太字数値（`**+140%**`, `**3.5x**`）による KPI ビッグナンバー表示
  - `> [!important]` などの Obsidian Callout による結論サマリー
- **発表者ノート & 資料配布対応**:
  - `> [!note]` を活用し、スライド本番の大画面には要点だけを表示、発表者には手元カンペ（`N` キー）を提供
  - 単一HTMLエクスポートやハンドアウト印刷（PDF）時には詳細解説として展開
- **スライドはみ出し（Overflow）防止**:
  - 1スライド1メッセージの徹底、`fit: auto`（自動縮小フィット）の付与

---

## ディレクトリ構成

```text
.agents/
└── skills/
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

### 方法 1: 特定の Obsidian Vault で使う場合（推奨）

お使いの Obsidian Vault のルートディレクトリで、本リポジトリの `.agents` フォルダを配置します。

```bash
cd /path/to/your-obsidian-vault

# 方法A: git clone して必要なスキルをコピー
git clone https://github.com/xhisashix/obsidian-presenter-skill.git /tmp/presenter-skill
mkdir -p .agents/skills
cp -R /tmp/presenter-skill/.agents/skills/create-presentation .agents/skills/
rm -rf /tmp/presenter-skill

# 方法B: Git Submodule として直接管理する場合
git submodule add https://github.com/xhisashix/obsidian-presenter-skill.git .agents/skills/create-presentation
```

### 方法 2: マシン全体（グローバル）で使う場合 (Antigravity)

すべてのワークスペースで利用可能にする場合は、グローバル設定ディレクトリに配置します。

```bash
mkdir -p ~/.gemini/config/skills
git clone https://github.com/xhisashix/obsidian-presenter-skill.git /tmp/presenter-skill
cp -R /tmp/presenter-skill/.agents/skills/create-presentation ~/.gemini/config/skills/
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
