---
header: "Tech Talk 2026"
accentColor: "#10b981"
fit: auto
---

# Obsidian Presenterで始める<br>エンジニアのためのスライド駆動開発
Markdownから直感的に生み出す美しきプレゼンテーション

発表者: @developer
イベント: 社内技術LT大会 2026

## アジェンダ

<!-- columns 3 step card -->

### 01. なぜスライド作りは辛いのか
エンジニアが抱える
プレゼン資料のジレンマ

### 02. Presenter Pluginの仕組み
標準Markdownを保ちつつ
美しいスライドを実現する設計

### 03. 現場でのTips & まとめ
実務で役立つ
カラム記法と配布テクニック

<!-- /columns -->

## 01. なぜスライド作りは辛いのか？

## エンジニアの資料作成におけるペイン

<!-- columns 2 card -->

### PowerPointの辛さ
- 手動のピクセル合わせに無限の時間を使う
- コードスニペットのシンタックスハイライトが死ぬ
- Gitでdiffが見れない（バイナリ地獄）

### 一般的なMarkdownスライドツールの辛さ
- 独自ディレクティブだらけでMarkdownとして読めない
- 非エンジニアに配る時に「どうやって開くの？」と言われる
- 印刷するとレイアウトがぐちゃぐちゃになる

<!-- /columns -->

## 02. Presenter Pluginの仕組み

## コアコンセプト: 標準Markdownの完全死守

<!-- columns 2:1 plain -->

### 記法ルール
- `# H1`: 表紙
- `## H2`: 各スライドの区切り
- `### H3`: カラムや小見出し
- `<!-- columns N -->`: マルチカラム

### 設計のこだわり
- [POINT] GitHubやObsidian通常表示でも綺麗に読める
- [POINT] 専用CLIや外部Node環境不要
- [POINT] エディタ横のリアルタイムプレビュー

<!-- /columns -->

## コードと解説の並列表示

<!-- columns 2:1 plain -->

### プラグイン起動コード
```typescript
// 選択ノートを即座にプレゼン化
const file = app.workspace.getActiveFile();
const content = await app.vault.read(file);
const presentation = parsePresentation(content);
new PresenterModal(app, presentation).open();
```

### 実装のポイント
- [重要] ASTパーサーによるCommonMark完全準拠
- コードブロック内の見出し・水平線を完全無視
- 250msデバウンスで入力追従

<!-- /columns -->

## 03. 現場でのTips & 配布

## 発表者ノート 兼 詳細解説 (`> [!note]`)

Obsidian標準のCallout `> [!note]` を書くだけで手元カンペになります。

```markdown
## 新アーキテクチャの概要
- マイクロサービスからモジュラーモノリスへの回帰

> [!note]
> プレゼン本番では大画面から自動で隠れ、手元カンペ（Nキー）に！
> 一方で単一HTML出力や配布印刷時には詳細解説として展開されます。
```

> [!tip] 登壇時のTips
> 発表時は `N` キーでノートを開閉、`G` キーで全スライド一覧（グリッド）を表示して質疑応答に備えましょう。

## まとめ

1. **思考の速度でスライドを書き、プレビューで即時確認**
2. **標準Markdown互換だからGitで差分管理＆レビュー可能**
3. **ブラウザで開ける単一HTML出力で、誰にでも一発共有**

> [!important] Try it now!
> 今日のLT資料もすべてObsidian Presenterで作成しました。
