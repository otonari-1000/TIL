# React開発におけるCSS Modulesの基本まとめ

## 1. CSS Modulesとは
CSS Modulesとは、React開発でよく使われる **CSSのクラス名をコンポーネント単位でスコープ化する仕組み** である。
通常のCSSではクラス名がグローバルに共有されるため、同じクラス名が複数のファイルに存在すると衝突する可能性がある。

### 通常のCSSの問題
```css
/* style.css */
.title {
  color: red;
}

/* other.css */
.title {
  color: blue;
}
```
両方が読み込まれると、どちらのスタイルが適用されるかはCSSの優先順位に依存してしまう。

### CSS Modulesの仕組み
CSS Modulesではビルド時にクラス名が自動的にユニークな名前へ変換される。
例：
```
title → Button_title__3fj2k
```
これにより、コンポーネントごとに安全にCSSを管理できる。

## 2. 基本的な使い方
### ① CSS Modulesファイルを作る

ファイル名は .module.css にする。
```
/* Button.module.css */

.button {
  background: blue;
  color: white;
  padding: 10px;
}

.text {
  font-size: 14px;
}
```

### ② Reactコンポーネントで読み込む
```javascript
import styles from "./Button.module.css";

function Button() {
  return (
    <button className={styles.button}>
      <span className={styles.text}>Click</span>
    </button>
  );
}

export default Button;
```

### ③ ブラウザでの実際のHTML

ビルド後はクラス名が自動変換される。
```html
<button class="Button_button__3fG1s">
  <span class="Button_text__1aH9d">Click</span>
</button>
```

## 3. 複数のCSS Modulesがある場合

同じディレクトリに複数の .module.css ファイルがあっても問題ない。

例：
```html
Button.module.css
Card.module.css
```
両方に .title クラスが存在していたとしても、CSS Modulesはクラス名を変換するため衝突しない。

例：
```
Button.module.css
.title → Button_title__abc

Card.module.css
.title → Card_title__xyz
```

## 4. importしていないCSSは適用されない

Reactコンポーネントでは importしたCSS Modulesのみ使用できる。

例：
```javascript
import styles from "./Button.module.css";
```
この場合
| CSSファイル           | 適用     |
| ----------------- | ------ |
| Button.module.css | 適用される  |
| Card.module.css   | 適用されない |

理由
→ Card.module.css を import していないため。

## 5. 複数のクラスを付ける方法
```javascript
<button className={`${styles.button} ${styles.primary}`}>
```
このようにテンプレート文字列で複数指定できる。

## 6. 同じ要素に異なるCSS Modulesを付けた場合
```javascript
import buttonStyles from "./Button.module.css";
import cardStyles from "./Card.module.css";

<h1 className={`${buttonStyles.title} ${cardStyles.title}`}>
```

この場合
- 両方のCSSが適用される
- CSSの優先順位により後から読み込まれたスタイルが優先される

## 7. import時の変数名は自由

CSS Modulesのimportでは、変数名は自由に決められる。

例1（一般的）
```javascript
import styles from "./Button.module.css";
```
例2
```javascript
import buttonStyles from "./Button.module.css";
```
例3
```javascript
import css from "./Button.module.css";
```
どれも同じ意味になる。

## 8. 実務でよく使われる書き方

Reactコミュニティの慣習として最も一般的なのは次の書き方。
```javascript
import styles from "./Button.module.css";
```
ただし複数のCSS Modulesを使う場合は、以下のように名前を分けることもある。
```javascript
import buttonStyles from "./Button.module.css";
import layoutStyles from "./Layout.module.css";
```


## まとめ
- CSS Modulesは クラス名の衝突を防ぐ仕組み
- .module.css ファイルとして作成する
- Reactでは import して使用する
- importしていないCSSは適用されない
- クラス名はビルド時にユニーク化される
- import時の変数名は自由に決められる
