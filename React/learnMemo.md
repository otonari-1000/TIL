# React学習メモ

## data-{任意データ名}/e.target.dataset.{任意データ名}
HTML部から情報を渡せる。
```html
<button type="button" onClick={handleRemove} data-id={item.id}>
    Remove
</button>
```
```javascript
const handleRemove = e => {
    setTodo(todo.filter(item =>
        item.id !== Number(e.target.dataset.id)
    ));
};
```