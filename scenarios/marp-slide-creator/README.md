# Marp Slide Creator

Marp を使用した Markdown 形式のプレゼンテーションスライドを作成するサンプルプロジェクトです。

## 🎯 概要

このプロジェクトは、**marp-slide-creator** という Agent Skills を活用して、オープンソースの **[Marp](https://marp.app/)** を使った Markdown フォーマットのスライド資料を作成するためのサンプルコードです。

### Marp とは？

Marp（Markdown Presentation Ecosystem）は、シンプルな Markdown ファイルから美しいプレゼンテーションを生成できるツールです。PowerPoint や Keynote のような専用ソフトを使わず、テキストエディタだけでスライドを作成できます。

**主なメリット：**

- 📝 Markdown 記法でシンプルに記述
- 🎨 テーマやカスタム CSS でデザインをカスタマイズ
- 📊 Mermaid 図（フローチャート、シーケンス図など）をサポート
- 📄 PDF、PowerPoint、HTML など複数形式にエクスポート可能
- 🔄 Git でバージョン管理が可能

---

## 📁 ディレクトリ構成

```
scenarios/marp-slide-creator/
├── Makefile              # タスクランナー（各種コマンドの定義）
├── README.md             # このファイル
├── slides/               # スライドの Markdown ファイルを格納
│   └── references.md     # サンプルスライド
├── themes/               # カスタムテーマの CSS を格納
│   └── custom.css        # カスタムテーマ
└── outputs/              # 出力ファイル（PDF, PPTX）の格納先
```

| フォルダ | 説明 |
|---------|------|
| `slides/` | スライドの Markdown ファイルを配置します。ここに `.md` ファイルを追加するとビルド対象になります |
| `themes/` | カスタムテーマの CSS ファイルを配置します。独自のデザインを適用できます |
| `outputs/` | ビルド後の PDF や PPTX ファイルが出力されます |

---

## 🚀 はじめ方

### 前提条件

- **Node.js** がインストールされていること（[ダウンロード](https://nodejs.org/en/download)）
- **Marp CLI** がインストールされていること（自動インストール可能）

### 1. 依存関係のインストール

```bash
make install-deps-dev
```

このコマンドで Marp CLI がグローバルにインストールされます。

### 2. プレビューサーバーの起動

```bash
make run
```

ブラウザでスライドをリアルタイムプレビューできます。Markdown ファイルを編集すると自動で反映されます。

### 3. ファイルのビルド

```bash
make build
```

PDF と PPTX 形式のファイルが `outputs/` フォルダに出力されます。

---

## 📋 Makefile コマンド一覧

`make help` を実行すると、利用可能なコマンドの一覧を確認できます。

| コマンド | 説明 |
|---------|------|
| `make help` | 利用可能なコマンドの一覧を表示します |
| `make install-deps-dev` | 開発に必要な依存関係（Marp CLI）をインストールします |
| `make run` | プレビューサーバーを起動します。ブラウザでスライドをリアルタイムに確認でき、ファイルの変更を監視して自動更新します |
| `make build` | PDF と PPTX の両方を一括でビルドします |
| `make pdf` | PDF 形式でスライドをエクスポートします |
| `make pptx` | PowerPoint (PPTX) 形式でスライドをエクスポートします。編集可能な PPTX を生成します（LibreOffice Impress が必要な場合があります） |
| `make clean` | `outputs/` フォルダ内のビルド成果物を削除します |
| `make ci-test` | CI テスト用のコマンド。クリーン → 依存関係インストール → ビルドを一括実行します |

---

## 📝 サンプルスライド

[slides/references.md](slides/references.md) にサンプルスライドが含まれています。

### Mermaid 図のサポート

このサンプルでは **Mermaid** を使用した図表の描画をサポートしています。シーケンス図、フローチャート、ER図などを Markdown 内に直接記述できます。

**サンプルコード例（シーケンス図）：**

```html
<script type="module">
import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@latest/dist/mermaid.esm.min.mjs';
mermaid.initialize({ startOnLoad: true });
</script>

<pre class="mermaid">
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    Bob-->>Alice: Hi Alice!
</pre>
```

Mermaid を使用するには、スライドの先頭で JavaScript を読み込み、`<pre class="mermaid">` タグ内に図の定義を記述します。

---

## 🎨 カスタムテーマ

[themes/custom.css](themes/custom.css) にカスタムテーマが定義されています。

### 主な特徴

- **日本語フォント対応**: Noto Sans JP、ヒラギノ角ゴなどを優先指定
- **アクセントカラー**: 青（#2C67E5）と赤（#DF3756）を定義
- **様々なレイアウトクラス**:
  - `title` - タイトルスライド用
  - `section` - セクション区切り用
  - `content-image-right` / `content-image-left` - 画像とテキストの分割レイアウト
  - `small-text` - 文字サイズを縮小

---

## 🤖 発展的な使い方: Playwright MCP によるデザイン修正

> **💡 このセクションは上級者向けです**  
> 基本的なスライド作成には不要ですが、AI を活用した自動デザイン改善に興味がある方向けの内容です。

### Playwright MCP とは？

**Playwright MCP** は、ブラウザ操作を AI エージェント（GitHub Copilot など）から制御できる仕組みです。

- **Playwright**: Web ブラウザを自動操作するためのツール
- **MCP (Model Context Protocol)**: AI エージェントが外部ツールと連携するための規格

これを使うと、スライドのプレビューを自動でキャプチャし、デザインの問題を検出・修正するフィードバックループを構築できます。

### セットアップ

Playwright MCP は `.vscode/mcp.json` で定義されているため、**VS Code を起動するとシームレスに利用できる状態**になっています。追加のセットアップは不要です。

### デザインフィードバックループの活用

`make run` でプレビューサーバーをローカル起動した状態で、Playwright MCP を使用してスライドにアクセスし、スクリーンショットを撮影することでデザインのフィードバックループを回すことができます。

**検出・修正できる問題の例：**

| 問題の種類 | 説明 |
|-----------|------|
| テキストの切れ目 | スライド枠をはみ出すテキストを検出 |
| 要素の重なり | 画像とテキストなど要素間の重なりを検出 |
| 配置の問題 | 中央揃え、余白の不均一などを検出 |
| コントラストの問題 | 背景色と文字色のコントラスト不足を検出 |

### ワークフロー例

1. **プレビューサーバーを起動**
   ```bash
   make run
   ```

2. **AI エージェントに依頼**
   - Playwright MCP がローカルサーバー（例: `http://localhost:8080`）にアクセス
   - スクリーンショットを撮影してデザインを分析
   - 問題点を特定し、Markdown や CSS を自動修正
   - 再度スクリーンショットを撮影して修正結果を確認

3. **反復的な改善**
   - 問題がなくなるまでフィードバックループを繰り返し
   - 最終的に `make build` で PDF/PPTX をエクスポート

### 参考

この手法は [anthropics/skills - pptx](https://github.com/anthropics/skills/blob/main/skills/pptx/SKILL.md) を参考にしています。

---

## 📚 参考資料

- [Marp 公式サイト](https://marp.app/)
- [Marp CLI GitHub](https://github.com/marp-team/marp-cli)
- [Mermaid 公式サイト](https://mermaid.js.org/)
- [Mermaid Examples](https://mermaid.js.org/syntax/examples.html)
