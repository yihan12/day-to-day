### 一、浏览器自带

```javascript
const num=12345.6789
 
num.toLocaleString();＝>"12,345.679"
```

### 二、正则匹配

```javascript
function format (num) {
 
    return (num+ '').replace(/(\d{1,3})(?=(\d{3})+(?:$|\.))/g,'$1,');
 
}
```
