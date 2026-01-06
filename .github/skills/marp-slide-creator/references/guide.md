# Marp 構文ガイド

このガイドでは、Marp で利用可能な Markdown 構文と機能を詳細に説明します。

## 目次

1. [基本構造](#基本構造)
2. [ディレクティブ](#ディレクティブ)
3. [画像構文](#画像構文)
4. [フラグメントリスト](#フラグメントリスト)
5. [高度な機能](#高度な機能)

---

## 基本構造

### スライドの区切り

スライドは水平線 `---` で区切ります。

```markdown
# スライド 1

スライド 1 の内容

---

# スライド 2

スライド 2 の内容

---

# スライド 3

スライド 3 の内容
```

### 基本的な Markdown 記法

Marp は標準的な Markdown 記法をサポートしています。

```markdown
# 見出し 1
## 見出し 2
### 見出し 3

**太字** と *斜体*

- 箇条書き 1
- 箇条書き 2

1. 番号付きリスト 1
2. 番号付きリスト 2

> 引用文

`インラインコード`

コードブロック
```

---

## ディレクティブ

ディレクティブは、スライドの設定やスタイルを制御する特別な命令です。

### グローバルディレクティブ

ファイルの先頭に YAML フロントマターとして記述し、全スライドに適用されます。

```yaml
---
marp: true
theme: default
paginate: true
header: 'ヘッダーテキスト'
footer: 'フッターテキスト'
size: 16:9
style: |
  section {
    background-color: #fff;
  }
---
```

#### 主要なグローバルディレクティブ

| ディレクティブ | 説明 | 値の例 |
|--------------|------|--------|
| `marp` | Marp を有効化 | `true` |
| `theme` | テーマを指定 | `default`, `gaia`, `uncover` |
| `paginate` | ページ番号を表示 | `true`, `false` |
| `header` | ヘッダーテキスト | `'プレゼンタイトル'` |
| `footer` | フッターテキスト | `'会社名'` |
| `size` | スライドサイズ | `16:9`, `4:3`, `1280x720` |
| `style` | カスタム CSS | CSS 文字列 |
| `backgroundColor` | 背景色 | `#ffffff`, `rgb(255,255,255)` |
| `backgroundImage` | 背景画像 | `url('image.jpg')` |
| `color` | テキスト色 | `#333333` |
| `class` | CSS クラス | `lead`, `invert` |
| `headingDivider` | 見出しで自動分割 | `1`, `2`, `[1, 2]` |

### ローカルディレクティブ

特定のスライドにのみ適用するディレクティブです。

#### HTML コメント形式

```markdown
<!-- _backgroundColor: lightblue -->
<!-- _color: #333 -->
<!-- _paginate: false -->
<!-- _header: '' -->
<!-- _footer: '' -->
<!-- _class: lead -->
```

#### スポットディレクティブ

`_` プレフィックスを使用すると、そのスライドのみに適用されます。

```markdown
---

<!-- _backgroundColor: #f5f5f5 -->
# このスライドだけ背景色が変わる

---

# このスライドは元の背景色に戻る
```

#### スコープディレクティブ

`_` なしで指定すると、以降のすべてのスライドに適用されます。

```markdown
---

<!-- backgroundColor: lightblue -->
# このスライド以降すべて背景色が変わる

---

# このスライドも背景色が適用される
```

### テーマ固有のクラス

#### default テーマ

- `lead`: タイトルスライド用（中央揃え、大きな見出し）
- `invert`: 色を反転（暗い背景、明るいテキスト）

```markdown
<!-- _class: lead -->
# プレゼンテーションタイトル

サブタイトル

---

<!-- _class: invert -->
# 暗いスライド
```

#### gaia テーマ

- `lead`: タイトルスライド用
- `invert`: 色を反転
- `gaia`: gaia スタイルを適用

#### uncover テーマ

- `lead`: タイトルスライド用
- `invert`: 色を反転

---

## 画像構文

### 基本的な画像挿入

```markdown
![代替テキスト](image.jpg)
```

### 画像サイズの指定

```markdown
![width:300px](image.jpg)
![height:200px](image.jpg)
![width:300px height:200px](image.jpg)
![w:300 h:200](image.jpg)
```

### パーセント指定

```markdown
![width:50%](image.jpg)
![w:80%](image.jpg)
```

### 背景画像

`bg` キーワードを使用して画像を背景に設定します。

#### 基本的な背景画像

```markdown
![bg](background.jpg)
# スライドタイトル
```

#### 背景画像のサイズ調整

```markdown
![bg contain](image.jpg)   <!-- アスペクト比を維持してフィット -->
![bg cover](image.jpg)     <!-- アスペクト比を維持して全体をカバー -->
![bg fit](image.jpg)       <!-- contain と同じ -->
![bg auto](image.jpg)      <!-- 元のサイズで表示 -->
![bg 50%](image.jpg)       <!-- 50% のサイズで表示 -->
```

#### 背景画像の配置

```markdown
![bg left](image.jpg)      <!-- 左側に配置（スプリットレイアウト） -->
![bg right](image.jpg)     <!-- 右側に配置（スプリットレイアウト） -->
![bg left:40%](image.jpg)  <!-- 左側 40% に配置 -->
![bg right:60%](image.jpg) <!-- 右側 60% に配置 -->
```

#### スプリットレイアウトの例

```markdown
![bg left:40%](image.jpg)

# 右側のコンテンツ

- ポイント 1
- ポイント 2
- ポイント 3
```

#### 複数の背景画像

```markdown
![bg](image1.jpg)
![bg](image2.jpg)
![bg](image3.jpg)

<!-- 横に並んで表示される -->
```

#### 背景画像のフィルター

```markdown
![bg blur](image.jpg)           <!-- ぼかし -->
![bg blur:5px](image.jpg)       <!-- ぼかし（強度指定） -->
![bg brightness:0.5](image.jpg) <!-- 明るさ -->
![bg contrast:1.5](image.jpg)   <!-- コントラスト -->
![bg grayscale](image.jpg)      <!-- グレースケール -->
![bg hue-rotate:90deg](image.jpg) <!-- 色相回転 -->
![bg invert](image.jpg)         <!-- 色反転 -->
![bg opacity:0.5](image.jpg)    <!-- 透明度 -->
![bg saturate:2](image.jpg)     <!-- 彩度 -->
![bg sepia](image.jpg)          <!-- セピア -->
![bg drop-shadow:5px,5px,10px,black](image.jpg) <!-- 影 -->
```

#### フィルターの組み合わせ

```markdown
![bg blur:3px brightness:0.7](image.jpg)
```

#### 背景色との併用

```markdown
<!-- _backgroundColor: rgba(0,0,0,0.5) -->
![bg opacity:0.3](image.jpg)

# 半透明の背景に白いテキスト
```

---

## フラグメントリスト

フラグメントリストを使用すると、リスト項目を順番に表示するアニメーション効果を追加できます。

### 基本構文

アスタリスク `*` を使用してフラグメント化します。

```markdown
# フラグメントリストの例

* 最初に表示される項目
* 次に表示される項目
* 最後に表示される項目
```

### 注意事項

- フラグメントリストは Marp CLI や Marp for VS Code でのプレゼンテーション時に有効
- PDF エクスポート時はすべての項目が表示された状態になる
- HTML エクスポート時にアニメーションが有効

### 番号付きフラグメントリスト

```markdown
1) 最初のステップ
2) 次のステップ
3) 最後のステップ
```

### ネストされたフラグメント

```markdown
* 親項目 1
  * 子項目 1-1
  * 子項目 1-2
* 親項目 2
  * 子項目 2-1
```

---

## 高度な機能

### 見出しによる自動分割

`headingDivider` ディレクティブを使用すると、指定したレベルの見出しで自動的にスライドを分割できます。

```yaml
---
marp: true
headingDivider: 2
---

# セクション 1

## スライド 1

内容

## スライド 2

内容

# セクション 2

## スライド 3

内容
```

### カスタム CSS

`style` ディレクティブでカスタム CSS を追加できます。

```yaml
---
marp: true
style: |
  section {
    font-family: 'Noto Sans JP', sans-serif;
  }
  h1 {
    color: #0066cc;
  }
  section.title {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
  }
---
```

カスタムクラスの使用：

```markdown
<!-- _class: title -->
# カスタムスタイルのタイトル
```

### スコープ付きスタイル

特定のスライドにのみスタイルを適用：

```markdown
<style scoped>
h1 {
  color: red;
}
</style>

# このスライドの見出しだけ赤色
```

### 数式の挿入

Marp は KaTeX を使用した数式をサポートしています。

```markdown
インライン数式: $E = mc^2$

ブロック数式:
$$
\sum_{i=1}^{n} x_i = x_1 + x_2 + \cdots + x_n
$$
```

### コードのシンタックスハイライト

````markdown
```python
def hello():
    print("Hello, World!")
```

```javascript
const greeting = () => {
  console.log("Hello, World!");
};
```
````

### テーブル

```markdown
| 列 1 | 列 2 | 列 3 |
|:-----|:----:|-----:|
| 左揃え | 中央 | 右揃え |
| データ 1 | データ 2 | データ 3 |
```

### 絵文字

```markdown
:smile: :rocket: :thumbsup:
```

### HTML の埋め込み

```markdown
<div style="display: flex; justify-content: center;">
  <img src="image.jpg" style="max-width: 50%;">
</div>
```

---

## ベストプラクティス

### 1. 一貫したスタイル

- すべてのスライドで同じフォントとカラースキームを使用
- グローバルディレクティブでスタイルを統一

### 2. 読みやすさの確保

- フォントサイズは最低 24px 以上
- 1 スライドの文字数は控えめに
- 十分なコントラストを確保

### 3. 画像の効果的な使用

- 背景画像は透明度を下げてテキストの可読性を確保
- スプリットレイアウトで画像とテキストをバランスよく配置

### 4. フラグメントの適切な使用

- 重要なポイントを順番に説明する場合に使用
- 使いすぎると逆効果になるため注意

### 5. コード例の提示

- シンタックスハイライトを活用
- 長いコードは避け、重要な部分のみ表示

---

## 参考リンク

- [Marp 公式サイト](https://marp.app/)
- [Marpit Framework](https://marpit.marp.app/)
- [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode)
- [Marp CLI](https://github.com/marp-team/marp-cli)
