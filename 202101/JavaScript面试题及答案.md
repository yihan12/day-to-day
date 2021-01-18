### 前言  
日常js面试题积累汇总。实时更新！

### 1.JavaScript的基本数据类型  

<details><summary><b>答案</b></summary>
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

<details><summary><b>答案</b></summary>
<p>

#### 答案:   
* `Object ` 
* `Function`  
* `Array`  
</p>
</details>  

***

### 3.Javascript基本数据类型和引用类型的特点  

<details><summary><b>答案</b></summary>
<p>

#### 答案:   
1.基本数据类型：值不可变；数据存放在栈区。  
2.引用数据类型：值是可变的；同时保存在栈内存和堆内存。
</p>
</details>  

***

### 4.检验JavaScript的数据类型的方法有哪些，以及使用它们的缺点  

<details><summary><b>答案</b></summary>
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

<details><summary><b>答案</b></summary>
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
