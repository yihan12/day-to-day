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

作用：返回指定位置的字符。

注意：字符串中第一个字符的下标是 0。如果参数 index 不在 0 与 string.length 之间，该方法将返回一个空字符串。

```javascript
let str = "1123"
console.log(str.charAt(0)) // "1"
console.log(str.charAt(5)) // ""
```

b)charCodeAt(index)

作用：返回在指定的位置的字符的 Unicode 编码。

注意：字符串中第一个字符的下标是 0。如果 index 是负数，或大于等于字符串的长度，则 charCodeAt() 返回 NaN。

```javascript
let str = "1123"
console.log(str.charCodeAt(0)) // 49
console.log(str.charCodeAt(5)) // NaN
console.log(str.charCodeAt(5)) // NaN
```

c)formCharCode(Unicode,Unicode,Unicode)

作用：用Unicode 编码创建一个字符串。

参数：一个或多个 Unicode 值，即要创建的字符串中的字符的 Unicode 编码。

注意：该方法是 String 的静态方法，字符串中的每个字符都由单独的数字 Unicode 编码指定。它不能作为您已创建的 String 对象的方法来使用。因此它的语法应该是 String.fromCharCode()，而不是myStringObject.fromCharCode()。该方法返回一个字符串，而不是一个  String 对象。

```javascript
console.log(String.fromCharCode(189, 43, 190, 61)); // "½+¾="
String.fromCharCode(65, 66, 67);   // "ABC"
String.fromCharCode(0x2014);       // "—"
String.fromCharCode(0x12014);      // "—"; 数字 1 被剔除并忽略
String.fromCharCode(8212);         // "—"; 8212 是 0x2014 的十进制表示
```

#### 2.位置方法

