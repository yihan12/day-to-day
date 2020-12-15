### 格式化json对象

```javascript
const list= {name: 'lisi',age: 14,id: 1}
JSON.stringify(list, null, "\t")
```

### 格式化json字符串

```javascript
let list= "{name: 'lisi',age: 14,id: 1}"
list = JSON.parse(list)
JSON.stringify(list, null, "\t")
```

### 输出 

```javascript
{
  name: 'lisi',
  age: 14,
  id: 1
}
```
