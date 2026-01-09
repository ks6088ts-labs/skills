# Marp スライド修正テクニック

このドキュメントでは、視覚的な問題を修正するための Marp 固有のテクニックを解説します。

## 問題別修正方法

### テキストの切れ目・はみ出し

#### コンテンツの削減

長すぎるテキストを短縮：

```markdown
<!-- 修正前 -->
- この項目は非常に長い説明文があり、スライドの端で切れてしまっています

<!-- 修正後 -->
- 項目の説明（端で切れないように短縮）
```

#### フォントサイズの調整

```markdown
<style scoped>
p {
  font-size: 0.9em;
}
li {
  font-size: 0.85em;
}
</style>
```

#### 複数スライドへの分割

コンテンツが多すぎる場合、`---` で新しいスライドに分割：

```markdown
## トピック（1/2）

- 項目 1
- 項目 2

---

## トピック（2/2）

- 項目 3
- 項目 4
```

### テキストの重なり

#### margin/padding の調整

```markdown
<style scoped>
h1 {
  margin-bottom: 30px;
}
ul {
  margin-top: 20px;
}
</style>
```

#### 要素の配置調整

```markdown
<div style="margin-top: 20px; margin-bottom: 20px;">
重なりを避けたいコンテンツ
</div>
```

### 配置の問題

#### セクション全体のパディング

```markdown
<style scoped>
section {
  padding: 40px 60px;
}
</style>
```

#### 個別要素の余白

```markdown
<div style="padding: 20px;">
境界から離したいコンテンツ
</div>
```

### コントラストの問題

#### テキスト色の変更

```markdown
<style scoped>
p {
  color: #333333;  /* より暗い色に */
}
</style>
```

#### 背景色の調整（ローカルディレクティブ使用）

```markdown
<!-- _backgroundColor: #f5f5f5 -->
```

#### 影の追加で読みやすく

```markdown
<style scoped>
h1, h2, p {
  text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
}
</style>
```

### 余白の不足

#### 行間の調整

```markdown
<style scoped>
p, li {
  line-height: 1.6;
}
</style>
```

#### 要素間のスペース

```markdown
項目 1

<br>

項目 2
```

#### リスト項目の間隔

```markdown
<style scoped>
li {
  margin-bottom: 15px;
}
</style>
```

## 画像関連の修正

### 画像サイズの制限

```markdown
![width:400px](image.png)
![height:300px](image.png)
![width:400px height:300px](image.png)
```

### 画像の配置

```markdown
<!-- 中央配置 -->
![center](image.png)

<!-- 背景画像として使用 -->
![bg right:40%](image.png)
```

## グローバル vs ローカルスタイル

### スコープ付きスタイル（そのスライドのみ）

```markdown
<style scoped>
/* このスライドのみに適用 */
</style>
```

### グローバルスタイル（全スライド）

フロントマター直後に配置：

```markdown
---
marp: true
---

<style>
/* 全スライドに適用 */
section {
  font-family: 'Noto Sans JP', sans-serif;
}
</style>
```

## 修正時のベストプラクティス

1. **最小限の変更**: 元のデザイン意図を尊重し、必要最小限の修正に留める
2. **scoped を優先**: グローバルスタイルより `<style scoped>` を使用
3. **段階的修正**: 大きな変更は避け、小さな調整を積み重ねる
4. **再検証**: 修正後は必ずスクリーンショットで確認
5. **コンテンツ保持**: テキストの内容は変更せず、見た目のみを調整
