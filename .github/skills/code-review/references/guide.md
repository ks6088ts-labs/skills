# コードレビューガイド

コードレビューを実施する際の詳細なガイドラインです。

## セキュリティレビュー

### チェック項目

- **機密データ**: パスワード、API キー、トークン、PII がコードやログに含まれていない
- **入力検証**: すべてのユーザー入力が検証・サニタイズされている
- **SQL インジェクション**: パラメータ化クエリを使用、文字列結合を使用していない
- **認証**: リソースアクセス前に適切な認証チェック
- **認可**: ユーザーがアクションを実行する権限があることを確認
- **暗号化**: 確立されたライブラリを使用、独自の暗号を実装していない
- **依存関係**: 既知の脆弱性がない

### 例

**❌ 悪い例: SQL インジェクション脆弱性**

```java
String query = "SELECT * FROM users WHERE email = '" + email + "'";
```

**✅ 良い例: パラメータ化クエリ**

```java
PreparedStatement stmt = conn.prepareStatement(
    "SELECT * FROM users WHERE email = ?"
);
stmt.setString(1, email);
```

**❌ 悪い例: シークレットの露出**

```javascript
const API_KEY = "sk_live_abc123xyz789";
```

**✅ 良い例: 環境変数を使用**

```javascript
const API_KEY = process.env.API_KEY;
```

## コード品質レビュー

### チェック項目

- **命名**: 変数、関数、クラスに説明的で意味のある名前
- **単一責任**: 各関数/クラスが 1 つのことをうまく行う
- **DRY**: コードの重複がない
- **関数サイズ**: 小さく焦点を絞った関数（理想的には 20-30 行未満）
- **ネスト**: 深くネストされたコードを避ける（最大 3-4 レベル）
- **マジックナンバー**: 定数を使用
- **エラーハンドリング**: 適切なレベルでの適切なエラー処理

### 例

**❌ 悪い例: 命名とマジックナンバー**

```javascript
function calc(x, y) {
    if (x > 100) return y * 0.15;
    return y * 0.10;
}
```

**✅ 良い例: 明確な命名と定数**

```javascript
const PREMIUM_THRESHOLD = 100;
const PREMIUM_DISCOUNT_RATE = 0.15;
const STANDARD_DISCOUNT_RATE = 0.10;

function calculateDiscount(orderTotal, itemPrice) {
    const isPremiumOrder = orderTotal > PREMIUM_THRESHOLD;
    const discountRate = isPremiumOrder ? PREMIUM_DISCOUNT_RATE : STANDARD_DISCOUNT_RATE;
    return itemPrice * discountRate;
}
```

**❌ 悪い例: サイレントエラーと汎用的な例外処理**

```python
def process_user(user_id):
    try:
        user = db.get(user_id)
        user.process()
    except:
        pass
```

**✅ 良い例: 明示的なエラーハンドリング**

```python
def process_user(user_id):
    if not user_id or user_id <= 0:
        raise ValueError(f"Invalid user_id: {user_id}")

    try:
        user = db.get(user_id)
    except UserNotFoundError:
        raise UserNotFoundError(f"User {user_id} not found in database")
    except DatabaseError as e:
        raise ProcessingError(f"Failed to retrieve user {user_id}: {e}")

    return user.process()
```

## テストレビュー

### チェック項目

- **カバレッジ**: クリティカルパスと新機能にテストがある
- **テスト名**: 何がテストされているかを説明する説明的な名前
- **テスト構造**: 明確な Arrange-Act-Assert または Given-When-Then パターン
- **独立性**: テストが相互に依存しない、外部状態に依存しない
- **アサーション**: 具体的なアサーションを使用、汎用的な assertTrue/assertFalse を避ける
- **エッジケース**: 境界条件、null 値、空のコレクションをテスト
- **モック**: 外部依存関係をモック、ドメインロジックはモックしない

### 例

**❌ 悪い例: 曖昧な名前とアサーション**

```typescript
test('test1', () => {
    const result = calc(5, 10);
    expect(result).toBeTruthy();
});
```

**✅ 良い例: 説明的な名前と具体的なアサーション**

```typescript
test('should calculate 10% discount for orders under $100', () => {
    const orderTotal = 50;
    const itemPrice = 20;

    const discount = calculateDiscount(orderTotal, itemPrice);

    expect(discount).toBe(2.00);
});
```

## パフォーマンスレビュー

### チェック項目

- **データベースクエリ**: N+1 クエリを避ける、適切なインデックスを使用
- **アルゴリズム**: ユースケースに適した時間/空間計算量
- **キャッシュ**: 高コストまたは繰り返し操作にキャッシュを活用
- **リソース管理**: コネクション、ファイル、ストリームの適切なクリーンアップ
- **ページネーション**: 大きな結果セットをページネーション
- **遅延ロード**: 必要な時だけデータをロード

### 例

**❌ 悪い例: N+1 クエリ問題**

```python
users = User.query.all()
for user in users:
    orders = Order.query.filter_by(user_id=user.id).all()  # N+1!
```

**✅ 良い例: JOIN または eager loading を使用**

```python
users = User.query.options(joinedload(User.orders)).all()
for user in users:
    orders = user.orders
```

## アーキテクチャレビュー

### チェック項目

- **関心の分離**: レイヤー/モジュール間の明確な境界
- **依存関係の方向**: 高レベルモジュールが低レベルの詳細に依存しない
- **インターフェース分離**: 小さく焦点を絞ったインターフェースを優先
- **疎結合**: コンポーネントが独立してテスト可能
- **高凝集度**: 関連する機能がグループ化されている
- **一貫したパターン**: コードベースで確立されたパターンに従う

## ドキュメントレビュー

### チェック項目

- **API ドキュメント**: パブリック API は目的、パラメータ、戻り値がドキュメント化
- **複雑なロジック**: 明らかでないロジックには説明的なコメント
- **README 更新**: 機能追加やセットアップ変更時に README を更新
- **破壊的変更**: 破壊的変更を明確にドキュメント化
- **使用例**: 複雑な機能には使用例を提供

## レビュー原則

1. **具体的に**: 正確な行、ファイルを参照し、具体的な例を提供
2. **コンテキストを提供**: なぜ問題なのか、潜在的な影響を説明
3. **解決策を提案**: 間違いだけでなく、修正されたコードを示す
4. **建設的に**: 作者を批判するのではなく、コードの改善に焦点
5. **良い実践を認める**: 適切に書かれたコードやスマートな解決策を認める
6. **実用的に**: すべての提案が即座の実装を必要とするわけではない
7. **関連するコメントをグループ化**: 同じトピックについて複数のコメントを避ける
