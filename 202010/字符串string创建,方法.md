### 字符串的创建

1.new String()

```javascript
let stringObj = new String("123")
console.log(stringObj) // object
```

这个是字符串对象，尽量不要这么做!!!!

2.创建基本的字符串值

```javascript
let stringStr = "123"
console.log(stringStr) // string
```

### 字符串的方法

#### 1.查找方法

a)charAt(index)

功能：返回指定位置的字符。

参数:字符在字符串中的下标。必须!!!!!

注释：字符串中第一个字符的下标是 0。如果参数 index 不在 0 与 string.length 之间，该方法将返回一个空字符串。

```javascript
let str = "1123"
console.log(str.charAt(0)) // "1"
console.log(str.charAt(0)) // ""
```
