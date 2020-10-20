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

注意：该方法将从后向前检索字符串，但返回是从起始位置 (0) 开始计算子字符串最后出现的位置。 看它是否含有字符串。

开始检索的位置在字符串的 start 处或字符串的结尾（没有指定 start 时）。

如果没有找到匹配字符串则返回 -1 

lastIndexOf() 方法是区分大小写的！
      
```javascript
let str="I am from runoob，welcome to runoob site.";
console.log(str.lastIndexOf("runoob")); // 28
```

#### 3.匹配方法

a)match(regexp)

作用: 方法检索返回一个字符串匹配正则表达式的结果。

参数:regexp一个正则表达式对象。如果传入一个非正则表达式对象，则会隐式地使用 new RegExp(obj) 将其转换为一个 RegExp 。如果你没有给出任何参数并直接使用match() 方法 ，你将会得到一 个包含空字符串的 Array ：[""] 。

返回值: 如果使用g标志，则将返回与完整正则表达式匹配的所有结果，但不会返回捕获组。
如果未使用g标志，则仅返回第一个完整匹配及其相关的捕获组（Array）。 在这种情况下，返回的项目将具有如下所述的其他属性。

```javascript
let str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
let regexp = /[A-E]/gi;

console.log(str.match(regexp));// ['A', 'B', 'C', 'D', 'E', 'a', 'b', 'c', 'd', 'e']
console.log(str.match());   // [""]
```

b)replace(regexp|substr, newSubStr|function)

作用: replace() 方法返回一个由替换值（replacement）替换部分或所有的模式（pattern）匹配项后的新字符串。模式可以是一个字符串或者一个正则表达式，替换值可以是一个字符串或者一个每次匹配都要调用的回调函数。如果pattern是字符串，则仅替换第一个匹配项。

参数:
regexp (pattern)
一个RegExp 对象或者其字面量。该正则所匹配的内容会被第二个参数的返回值替换掉。
substr (pattern)
一个将被 newSubStr 替换的 字符串。其被视为一整个字符串，而不是一个正则表达式。仅第一个匹配项会被替换。
newSubStr (replacement)
用于替换掉第一个参数在原字符串中的匹配部分的字符串。该字符串中可以内插一些特殊的变量名。参考下面的使用字符串作为参数。
function (replacement)
一个用来创建新子字符串的函数，该函数的返回值将替换掉第一个参数匹配到的结果。参考下面的指定一个函数作为参数。

```javascript
function replacer(match, p1, p2, p3, offset, string) {
  // p1 is nondigits, p2 digits, and p3 non-alphanumerics
  return [p1, p2, p3].join(' - ');
}
let newString = 'abc12345#$*%'.replace(/([^\d]*)(\d*)([^\w]*)/, replacer);
console.log(newString);  // abc - 12345 - #$*%

let re = /apples/gi;
let str = "Apples are round, and apples are juicy.";
let newstr = str.replace(re, "oranges");
console.log(newstr);// oranges are round, and oranges are juicy.
```

c)str.split([separator[, limit]])

作用: split() 方法使用指定的分隔符字符串将一个String对象分割成子字符串数组，以一个指定的分割字串来决定每个拆分的位置。 

参数:
separator
指定表示每个拆分应发生的点的字符串。separator 可以是一个字符串或正则表达式。 如果纯文本分隔符包含多个字符，则必须找到整个字符串来表示分割点。如果在str中省略或不出现分隔符，则返回的数组包含一个由整个字符串组成的元素。如果分隔符为空字符串，则将str原字符串中每个字符的数组形式返回。
limit
一个整数，限定返回的分割片段数量。当提供此参数时，split 方法会在指定分隔符的每次出现时分割该字符串，但在限制条目已放入数组时停止。如果在达到指定限制之前达到字符串的末尾，它可能仍然包含少于限制的条目。新数组中不返回剩下的文本。

注意：如果使用空字符串(“)作为分隔符，则字符串不是在每个用户感知的字符(图形素集群)之间，也不是在每个Unicode字符(代码点)之间，而是在每个UTF-16代码单元之间。这会摧毁代理对。
