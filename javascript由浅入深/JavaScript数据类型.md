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
* `Array`  
* `Function`  
* `Date`  
* `RegExp`  

> 注：除了`Array`、`Function`、`Date`、`RegExp`属于特殊的对象数据类型。

### 包装类型（三种）  

* `Number`  
* `String`  
* `Boolean`  

```javascript
const Booln = new Boolean(true)
console.log(Booln) // Boolean {true}
console.log(Booln === true) // false
console.log(typeof Booln) // object
console.log(Booln instanceof Object) // true
console.log(Object.prototype.toString.call(Booln)) // [object Boolean]
console.log(Object.prototype.toString(Booln)) // [object Object]

const str = new String('123')
console.log(str) // String {"123"}
console.log(str === '123') // false
console.log(typeof str) // object
console.log(str instanceof Object) // true
console.log(Object.prototype.toString.call(str)) // [object String]
console.log(Object.prototype.toString(str)) // [object Object]

const num = new Number(123)
console.log(num) // String {"123"}
console.log(num === 123) // false
console.log(typeof num) // object
console.log(num instanceof Object) // true
console.log(Object.prototype.toString.call(num)) // [object Number]
console.log(Object.prototype.toString(num)) // [object Object]
```

> 1、引用类型和基本包装类型的区别就是对象的生存期;  
> 2、自动创建的基本包装类型的对象，只存在于一行代码的执行瞬间，然后立即被销毁；  
> 3、意味着我们不能在运行时为基本类型添加属性和方法。  

基本类型的字面量写法，很明显不能为基本类型添加属性和方法
```javascript
const s1 = 'name.Lee'
s1.name = 'lee'
s1.age = function () {
  return 100
}
console.log(s1.substring(5)) // =>Lee
console.log(typeof s1) // string
console.log(s1.name) // undefined
console.lgo(s1.age()) // Uncaught TypeError: s1.age is not a function
```

new运算符写法,既能添加方法属性，还能使用它的内置方法`substring`
```javascript
const s2 = new String('name.Lee')
s2.name = 'lee'
s2.age = function () {
  return 100
}
console.log(s2.substring(5)) // =>Lee
console.log(typeof s2) // object
console.log(s2.name) // lee
console.log(s2.age()) // 100
```

### `null`和`undefined`的区别  

[undefined与null的区别---阮一峰](https://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html)  

笔记：  
> 1、在`!`运算符处理后，自动转成`true`

```javascript
console.log(!null) // true
console.log(!undefined) // true
console.log(!undefined === !null) // true
```

> 2、相等，但是不全等  

```javascript
console.log(null == undefined) // true
console.log(null === undefined) // false
```

> 3、最初设计：`null`是一个表示"无"的对象，转数值为`0`;`undefined`是一个表示"无"的原始值，转数值为`NaN`。

```javascript
console.log(Number(undefined)) //NaN
console.log(Number(5 + undefined)) //NaN

console.log(Number(null)) //0
console.log(Number(5 + null)) //5
```

> 4、两者`typeof`区别：  

```javascript
console.log(typeof undefined) //undefined
console.log(typeof null) //object
```

> 5、现在的用法：  
> `null`:表示"没有对象"，即此处不应该有值。(表示被赋值过的对象，刻意把一个对象赋值为`null`，故意表示其为空，不应有值。)  
> （1）作为函数的参数，表示该函数的参数不是对象;  
> （2）作为对象原型链的终点。  
> `undefined`:表示"缺少值"，即此处应该有一个值，但是没有定义。  
> （1）变量被声明了，但没有赋值时，就等于undefined;  
> （2) 调用函数时，应该提供的参数没有提供，该参数等于undefined;  
> （3）对象没有赋值的属性，该属性的值为undefined;  
> （4）函数没有返回值时，默认返回undefined。  

### 判断JavaScript数据类型的方式(四种)   

* `typeof`  
* `instanceof`    
* `toString`  
* `jquery`

#### `typeof`适用场景： 

```javascript
console.log(typeof undefined) //undefined
console.log(typeof 123) //number
console.log(typeof '123') //string
console.log(typeof true) //boolean
console.log(typeof Symbol()) //symbol
console.log(typeof function () {}) //function
```

#### `typeof`不适用场景： 

```javascript
console.log(typeof new Date()) //object
console.log(typeof /^\d*$/) //object
console.log(typeof {}) //object
console.log(typeof []) //object
console.log(typeof null) //object
```  

#### 面试题：  

```javascript
let foo = function bar() {
  return 123
}
console.log(typeof bar) // undefined
console.log(typeof foo)
// console.log(typeof bar()) // Uncaught ReferenceError: bar is not defined
console.log(typeof foo()) // number
```
