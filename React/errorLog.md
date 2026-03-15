# Reactエラー解決履歴
## 配列が空のとき表示を変える
### NG例
```javascript
<ul>
                {if(todo !== []) {
                    '未完了のタスクはありません'
                } else {todo.map(item => (
                    <li key={item.id} className={item.isDone ? 'done' : ''}>
                        {item.title}
                    </li>
                }
                ))}
</ul>
```
- JSX内ではif文は使えない  
JSX の { ... } の中には「式（expression）」しか書けませんが、if は「文（statement）」なので構文エラーになります。
正しくは 三項演算子（condition ? a : b） や 論理演算子（&&） を使います。
- todo !== [] は常に true になる  
JavaScript で配列同士を === / !== で比較すると、参照が同じかどうかだけを比較します。
[] と [] は別オブジェクトなので常に異なり、常に true になり、意図通りに「空チェック」できません。

### 修正
```javascript
<ul>
    {todo.length === 0 && '未完了のタスクはありません'}
    {todo.length > 0 &&
        todo.map(item => (
            <li key={item.id} className={item.isDone ? 'done' : ''}>
                {item.title}
            </li>
        ))}
</ul>
```

## ulのリストマーカー（●）が「外側」に描画される
``<ul> / <ol>`` のデフォルトはマーカーが枠の外側に描かれる
```css
list-style-position: outside;
```
解決法
```css
.todolist {
  list-style-position: inside;
}
```