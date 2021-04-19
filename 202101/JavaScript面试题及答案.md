### 前言  
日常js面试题积累汇总。实时更新！

### 1.JavaScript的基本数据类型  

<details><summary><b></b></summary>
<p>

#### 答案:   
`Number`、`String`、`Boolean`、`Null`、`Undefined`、`Symbel`（ES6新增）  
Object是JavaScript中所有对象的父对象  
数据封装类对象：`Object`、`Array`、`Boolean`、`Number`、和`String`  
其他对象：`Function`、`Arguments`、`Math`、`Date`、`RegExp`、`Error`  
</p>
</details>  

***

### 2.JavaScript的引用类型  

<details><summary><b></b></summary>
<p>

#### 答案:   
* `Object ` 
* `Function`  
* `Array`  
</p>
</details>  

***

### 3.Javascript基本数据类型和引用类型的特点  

<details><summary><b></b></summary>
<p>

#### 答案:   
1.基本数据类型：值不可变；数据存放在栈区。  
2.引用数据类型：值是可变的；同时保存在栈内存和堆内存。
</p>
</details>  

***

### 4.检验JavaScript的数据类型的方法有哪些，以及使用它们的缺点  

<details><summary><b></b></summary>
<p>

#### 答案:   
* 1.`typeof`：不能判断null和区分Array/Date/RegExp  
* 2.`instanceof`：无法检测null和undefined；未必准确（是否处于处于原型链上的方法不准确）；无法判断字面量方式创建的基本数据类型；    
* 3.`constructor`：无法检测null和undefined；未必准确
* 4.`Object.prototype.toString.call()`：无；全能方法；  
</p>
</details>  

***

### 5.JavaScript基本数据类型和非基本数据类型的区别  

<details><summary><b></b></summary>
<p>

#### 答案:   
* 1.目前JS中有6种基本数据类型：`Undefined`、`Null`、`Boolean`、`Number`、`String`和`Symbel`（ES6新增）。还有一种复杂数据类型----`Object`,`Object`本质上是由一组无序的名值对组成的，`Object`、`Fuction`、`Array`则属于引用类型。  
* 2.基本数据类型是不可变的，而非基本数据类型是可变的。 
* 3.基本数据类型是不可变的，因为一旦它们创建就无法更改。但是非基本数据类型可更改，意味着一旦创建对象，就可以更改它。  
* 4.将基本数据类型与其值进行比较，这意味着如果两个值具有相同的数据类型，并具有相同的值，那么它们是严格相等的。  
* 5.非基本数据类型不与值进行比较。例如，如果两个对象具有相同的属性和值，则它们严格不相等。 
</p>
</details>  

***  

### 6.instanceof操作符  

<details><summary><b></b></summary>
<p>

#### 答案:   
判断对象属于某一个类，回去查找对象的constructor的prototype
</p>
</details>  

***  

### 7.new操作符的作用  

<details><summary><b></b></summary>
<p>

#### 答案:   
* 新生了一个对象  
* 链接到原型(该对象继承该函数的原型，更改了原型链的指向)   
* 绑定this  
* 返回对象  

```javascript
function newCreate(){
  // 创建一个空白对象
  let obj = new Object();
  // 获得构造函数
  let Con = [].shift.call(arguments);
  // 链接到原型
  obj.__proto__ = Con.prototype; 
  // 绑定this,执行构造函数
  let result = Con.apply(obj,arguments);
  // 确保new出来的是个对象
  return typeof result === 'object' ? result : obj;
}
```
</p>
</details>  

***  

### 8.作用域和作用域链  

<details><summary><b></b></summary>
<p>

#### 答案:   
[静态作用域与动态作用域](https://github.com/yihan12/day-to-day/blob/master/202101/%E8%AF%8D%E6%B3%95%E4%BD%9C%E7%94%A8%E5%9F%9F%E5%92%8C%E5%8A%A8%E6%80%81%E4%BD%9C%E7%94%A8%E5%9F%9F.md)  
#### 1.作用域  

* 种类：JS中有三种作用域，全局作用域，函数作用域，ES6新推出的块级作用域。  
* 概念：一个变量的可访问规则，在函数创建的时候就已经创建好作用域，整个JS文件执行有一个最外层的全局作用域（window）。  
* 使用：本作用域内部的所有变量都可以在本作用域内部访问，外部无法访问。内部可访问上级作用域变量，本作用域内部所使用的var声明的变量会有一个作用域提升的过程，let、const声明的变量没有变量提升。  

#### 2.作用域链  

* 一个变量的访问规则的链式操作  
* 可以把它理解成包含自身变量对象和上级变量对象的列表，可以通过[[Scope]]属性查找上级变量  
* 当访问一个变量时，现在本作用域内查找，如果没有，就回去上一级作用域查找，直到全局作用域window下面，都没有返回undefined  
</p>
</details>  

***  

### 9.闭包  

<details><summary><b></b></summary>
<p>

#### 答案:   
1.特点：  

* 内层作用域可以访问外层作用域的变量  
* 闭包就是可以读取其他函数内部变量的函数  
* 函数A返回一个函数B，并且函数B中使用了函数A的变量，函数B就称为闭包  
* 闭包函数引用的变量是存储在堆上的，所以说，当闭包函数弹出调用栈后，闭包返回的函数依然能够调用到闭包函数的变量  

2.优点  

* 使用闭包能够形成独立的空间，延长变量的生命周期，保存中间状态值  
* 可以封装一些私有变量，外部无法直接访问（例如用户登录状态计数器）创建立即执行函数（闭包）实现js模块化封装  
* 解决var声明的循环语句变量无法长久保存的问题  

3.缺点  

* 滥用闭包会导致内存泄漏，因为闭包中引用的包裹函数的变量都永远不会被释放，所以我们应该在必要的时候，及时释放这个闭包函数，将不再使用的闭包引用变量设置为null  
* 由于函数闭包的变量都保存在内存中，会导致内存消耗大  
</p>
</details>  

***

### 10.null和undefined的区别  

<details><summary><b></b></summary>
<p>

#### 答案:   
`undefined`: 表示缺少值，即此处应该有值，但没有定义。   
* 声明一个变量,这个变量的值就自动被赋予了`undefined`;  

```javascript
var a;
// undefined
```  

* 调用函数时，应该被提供的参数没有提供，该参数等于`undefined`;  

* 对象没有赋值的属性，该属性为`undefined`;  

* 函数没有返回值，默认返回`undefined`;  

`null`：表示没有对象，即此处不应该有值。  
* 作为函数的参数，表示该函数的参数不是对象;  
* 作为对象原型链的终点。  

其他方面的区别：   
（1）数据类型的区别  

```javascript
console.log(typeof undefined); // undefined
console.log(typeof null); // Object
```

**注意：这是JS设计的一个失误**  

（2）转为数值的区别  

```javascript
let num1 = 5 + null; // 5
let num2 = 5 + undefined; // NaN
```

（3)`null !== undefined` 

```javascript
console.log(null == undefined); // true
console.log(null === undefined); // false
```
</p>
</details>  

***

### 11.原型和原型链  

<details><summary><b></b></summary>
<p>

#### 答案:   
[原型和原型链](https://github.com/yihan12/day-to-day/blob/master/202012/%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%8E%9F%E5%9E%8B%E9%93%BE%E4%B8%80%E7%9F%A5%E5%8D%8A%E8%A7%A3.md)  
</p>
</details> 

***

### 12.var，let和const有什么区别

<details><summary><b></b></summary>
<p>

#### 答案:   
* **相同点**：`var`,`let`,`const`声明的变量，是不能被`delete`的;
* **区别**：
**变量提升**：`var`声明的变量存在变量提升，即变量可以在声明之前调用，值为undefined；  
`let`,`const`不存在变量提升，即它们声明的变量一定要在声明后使用，否则会报错。  

**暂时性死区**：`var`不存在暂时性死区；`let`、`const`存在暂时性死区，只有等声明变量后，才可以获取和使用该变量。  

**重复声明**：`var`允许重复声明；`lat`、`const`在同一作用域不允许重复声明。  

**修改声明的变量**：`var`和`let`可以修改声明的变量；`const`声明一个只读常量，一旦声明，常量的值就不能改变。

</p>
</details> 

***

### 13.`call()`、`apply()`、`bind()`的区别和作用

<details><summary><b></b></summary>
<p>

#### 答案:   
> 作用：(改变this的指向)都是在函数执行的时候，改变函数的运行环境，也就是改变函数的执行上下文；第一个参数都是改变运行环境的变量；如果第一个函数没有或者为null、undefined,则默认指向全局window。 

区别：（接受参数的方式不同、改变this指向后的处理不同）  
`call()`从第二个函数开始，第一个参数会依次传递给调用函数(参数列表);改变指向后原函数会立即执行，且此方法只是临时改变this指向一次。    
```javascript
Function.call(obj, varl, var2， var3)
```  
`apply()`的第二个参数是数组，数组的每一个成员会依次传递给调用函数（参数数组）;改变指向后原函数会立即执行，且此方法只是临时改变this指向一次。    
```javascript
Function.apply(obj, [varl, var2， var3])
```
`bind()`从第二个函数开始，第一个参数会依次传递给调用函数(参数列表);改变指向后原函数不会立即执行，会返回一个永久改变this指向的函数。  
```javascript
Function.call(obj, varl, var2， var3)
```

</p>
</details> 

***

### 14.`cookie`、`localStorage`、`sessionStorage`的异同点

<details><summary><b></b></summary>
<p> 

#### 答案:   
| 分类 | 生命周期 | 存储容量 | 储存位置 |  
|:---:|:---:|:---:|:---:|
</p>
</details> 
