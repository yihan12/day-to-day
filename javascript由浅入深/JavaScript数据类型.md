# JavaScript数据类型

### JavaScript基本数据类型/原始数据类型/值类型（六种）  

* `Null`  
* `Undefined`  
* `String`   
* `Number`  
* `Boolean`  
* `Symbol`  

> 注：`Symbol` 是 ES6 引入了一种新的原始数据类型，表示独一无二的值。

> 注：在es10中加入了原始数据类型`BigInt`，现已被最新Chrome支持  

```javascript
console.log(BigInt) // ƒ BigInt() { [native code] }
console.log(typeof 1n) // bigint
console.log(1n instanceof BigInt) //false
console.log(Object.prototype.toString.call(1n)) //[object BigInt]
console.log(jQuery.type(1n)) // bigint
```

[BigInt MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/BigInt)

### 引用数据类型/对象数据类型（一种）  

* `Object`  

> 除了`Array`、`Function`、`Date`、`RegExp`属于特殊的对象数据类型。
