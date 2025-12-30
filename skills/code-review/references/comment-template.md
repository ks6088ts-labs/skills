# コメントテンプレート

レビューコメントを記載する際のテンプレートと例です。

## 基本フォーマット

```markdown
**[優先度] カテゴリ: 簡潔なタイトル**

問題または提案の詳細な説明。

**なぜ重要か:**
影響や提案の理由の説明。

**修正案:**
[該当する場合はコード例]

**参考:** [関連ドキュメントや標準へのリンク]
```

## 優先度別テンプレート

### 🔴 CRITICAL

マージをブロックする重大な問題に使用。

```markdown
**🔴 CRITICAL - セキュリティ: SQL インジェクション脆弱性**

45 行目のクエリがユーザー入力を直接 SQL 文字列に結合しており、
SQL インジェクション脆弱性を作成しています。

**なぜ重要か:**
攻撃者が email パラメータを操作して任意の SQL コマンドを実行でき、
すべてのデータベースデータが露出または削除される可能性があります。

**修正案:**

// 修正前:
query = "SELECT * FROM users WHERE email = '" + email + "'"

// 修正後:
PreparedStatement stmt = conn.prepareStatement(
  "SELECT * FROM users WHERE email = ?"
);
stmt.setString(1, email);

**参考:** OWASP SQL Injection Prevention Cheat Sheet
```

```markdown
**🔴 CRITICAL - 正確性: データ破損リスク**

120 行目のトランザクション処理で、エラー発生時にロールバックが
呼び出されていません。

**なぜ重要か:**
部分的なデータ書き込みが発生し、データの整合性が失われる可能性があります。

**修正案:**

try {
  await transaction.begin();
  // 処理
  await transaction.commit();
} catch (error) {
  await transaction.rollback();  // 追加
  throw error;
}
```

### 🟡 IMPORTANT

議論が必要な重要な問題に使用。

```markdown
**🟡 IMPORTANT - テスト: クリティカルパスのテストカバレッジ不足**

`processPayment()` 関数は金融取引を処理しますが、
返金シナリオのテストがありません。

**なぜ重要か:**
返金はお金の動きを伴い、金融エラーやデータ不整合を防ぐために
徹底的にテストされるべきです。

**修正案:**

test('注文がキャンセルされた場合、全額返金を処理する', () => {
  const order = createOrder({ total: 100, status: 'cancelled' });

  const result = processPayment(order, { type: 'refund' });

  expect(result.refundAmount).toBe(100);
  expect(result.status).toBe('refunded');
});
```

```markdown
**🟡 IMPORTANT - パフォーマンス: N+1 クエリ問題**

getUsersWithOrders 関数で、ユーザーごとに個別の注文クエリが
実行されています（N+1 問題）。

**なぜ重要か:**
ユーザー数が増えるとクエリ数が線形に増加し、
レスポンス時間が大幅に悪化します。

**修正案:**

// 修正前:
const users = await User.findAll();
for (const user of users) {
  user.orders = await Order.findAll({ where: { userId: user.id } });
}

// 修正後:
const users = await User.findAll({
  include: [{ model: Order }]
});
```

### 🟢 SUGGESTION

非ブロッキングな改善提案に使用。

```markdown
**🟢 SUGGESTION - 可読性: ネストした条件を簡素化**

30-40 行目のネストした if 文がロジックを追いにくくしています。

**なぜ重要か:**
シンプルなコードは保守、デバッグ、テストが容易です。

**修正案:**

// ネストした if の代わりに:
if (user) {
  if (user.isActive) {
    if (user.hasPermission('write')) {
      // do something
    }
  }
}

// ガード節を検討:
if (!user || !user.isActive || !user.hasPermission('write')) {
  return;
}
// do something
```

```markdown
**🟢 SUGGESTION - ベストプラクティス: マジックナンバーを定数化**

87 行目の `timeout: 30000` はマジックナンバーです。

**なぜ重要か:**
定数に意味のある名前を付けることで、コードの意図が明確になり、
変更時の影響範囲も把握しやすくなります。

**修正案:**

const API_TIMEOUT_MS = 30000;

// 使用箇所
fetch(url, { timeout: API_TIMEOUT_MS });
```

## カテゴリ一覧

コメントで使用する主なカテゴリ:

| カテゴリ     | 説明                                 |
| ------------ | ------------------------------------ |
| セキュリティ | 脆弱性、認証/認可、機密データ        |
| 正確性       | ロジックエラー、データ整合性         |
| テスト       | テストカバレッジ、テスト品質         |
| パフォーマンス | N+1、メモリリーク、アルゴリズム      |
| コード品質   | SOLID 違反、重複、複雑性             |
| 可読性       | 命名、構造、フォーマット             |
| アーキテクチャ | 設計パターン、依存関係               |
| ドキュメント | コメント、API ドキュメント           |
| ベストプラクティス | 慣習、イディオム                 |
