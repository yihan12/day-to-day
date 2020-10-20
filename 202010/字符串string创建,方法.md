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

a)indexOf(searchValue，fromIndex)

作用: indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置。如果没有找到匹配的字符串则返回 -1。

注意：indexOf() 方法区分大小写。searchvalue	必需。规定需检索的字符串值。fromIndex 可选的整数参数。规定在字符串中开始检索的位置。它的合法取值是 0 到 string Object.length - 1。如省略该参数，则将从字符串的首字符开始检索。

语法: string.indexOf(searchvalue,start)

```javascript
let str="Hello world, welcome to Beijing.";
console.log(str.indexOf("welcome")); // 13
```

b)lastIndexOf(searchValue，fromIndex)

作用: lastIndexOf() 方法可返回一个指定的字符串值最后出现的位置，如果指定第二个参数 start，则在一个字符串中的指定位置从后向前搜索。

注意： 该方法将从后向前检索字符串，但返回是从起始位置 (0) 开始计算子字符串最后出现的位置。 看它是否含有字符串。

      开始检索的位置在字符串的 start 处或字符串的结尾（没有指定 start 时）。

      如果没有找到匹配字符串则返回 -1 

      lastIndexOf() 方法是区分大小写的！
      
```javascript
let str="I am from runoob，welcome to runoob site.";
console.log(str.lastIndexOf("runoob")); // 28
```
