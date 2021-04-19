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
| 分类 | 生命周期 | 存储容量 | 储存位置 | 应用场景 | 浏览器兼容性 |    
|:---:|:---:|:---:|:---:|:---:|:---:|       
| cookie | 默认保存在内存中,随浏览器关闭失效(如果设置过期时间，在到过期时间会失效) | 4kb | 保存在客户端每次请求都会带上 | 用户的部分不重要信息或者登录信息 | 兼容性完全没问题 |    
| localStorage | 理论上永久有效,除非主动清除 | 4.98M(不同浏览器情况不同，safari2.49M)| 保存在客户端，不与服务端交互，节省网络流量 | 适合持久化缓存数据，比如页面的偏好配置等 | IE8+以上的浏览器 |   
| sessionStorage | 仅在当前网页会话下有效，关闭页面或浏览器后会被清除 | 4.98M(部分浏览器没有限制) | 保存在客户端，不与服务端交互，节省网络流量 | 适合一次性临时数据缓存 | IE8+以上的浏览器 |    

注意点：  
* `localStorage`写入的时候如果超出容量会报错，但之前保存的数据不会丢失。  
* `localStorage`存储量快要满的时候，`getItem`的性能会急剧下降。  
* `webStorage(localStorage、sessionStorage)`在保存复杂数据类型时，较为依赖`JSON.stringify()`在移动端性能问题比较明显。 
</p>
</details> 

***

### 15.HTTP、HTTPS有什么联系，端口号是多少？

<details><summary><b></b></summary>
<p> 

#### 答案:   
HTTP通常承载于TCP之上，在HTTP和TCP之间添加了一个安全协议层（SSL或TLS），这个时候，就变成了我们常说的HTTPS。HTTP默认端口号80，HTTPS默认端口号443。  
</p>
</details>

***

### 16.HTTP、HTTPS有什么联系，端口号是多少？为什么HTTPS更安全?

<details><summary><b></b></summary>
<p> 

#### 答案:   
HTTP:是客户端和服务端之间数据传输的格式规范，表示超文本传输协议。HTTP通常承载于TCP之上，在HTTP和TCP之间添加了一个安全协议层（SSL或TSL），这个时候，就变成了我们常说的HTTPS。HTTP默认端口号80，HTTPS默认端口号443。  
在网络请求中，需要很多服务器，路由器的转发。其中的节点都可能篡改信息，而如果使用HTTPS，密钥在终点站才有。HTTPS之所以安全，是因为它利用SSL/TLS协议传输。它包含证书、卸载、流量转发、负载均衡、页面适配、浏览器适配、refer传递等技术、保障了传输过程中的安全性。
</p>
</details>  

***

### 17.HTTP/2

<details><summary><b></b></summary>
<p> 

#### 答案:   
> 引入服务器端推送（server push）的概念,它允许服务器端在客户端需要数据之前主动将数据发送到客户端缓存中，从而提高性能。  
> 提供更多的加密支持。  
> 使用多路线路，允许多个消息在一个连接上同时交差。  
> 增加了头压缩（header compression），因此请求非常小，请求和响应的header都只会占用很小的带宽。
</p>
</details>  

***

### 18.HTTP常见状态码

<details><summary><b></b></summary>
<p> 

#### 答案:   
* 100 Continue表示继续，一般在发送post请求时，已发送了HTTP header之后，服务端将会缓存此信息，表示确认，之后发送具体参数信息。  
* 200 OK表示正常返回信息。  
* 201 Created表示请求成功并且服务器创建了新资源。  
* 202 Accepted表示服务器已接受请求，但尚未处理。  
* 301 Moved Permanently表示请求的网页已永久移动到新位置。  
* 302 Found表示临时重定向。  
* 303 See Other表示临时重定向，且总是使用GET请求新的URI。  
* 304 Not Modified表示自从上次请求后，请求网页未修改。  
* 400 Bad Request表示服务器无法理解请求格式，客户端不应当尝试再次使用相同的内容发起请求。  
* 401 Unauthorized表示请求未授权。  
* 403 Forbidden表示禁止访问。  
* 404 Not Found表示找不到如何与URI匹配的资源。  
* 500 Internet Server error表示最常见的服务端的错误。  
* 503 Service Unavailable表示服务端暂时无法处理请求（可能是过载或维护）。  

</p>
</details>  

***

### 19.无状态协议？如何克服无状态协议缺陷？
<details><summary><b></b></summary>
<p> 

#### 答案:   
无状态协议对于事务处理没有记忆功能，缺少状态意味着如果后续需要处理，需要前面提供信息。  
克服无状态协议缺陷的办法就是通过cookie和会话保存信息。

</p>
</details>  

***

### 20.HTTP请求报文和响应报文包括哪些部分？
<details><summary><b></b></summary>
<p> 

#### 答案:   
请求报文：  
* 请求行，包含请求方法、URI、HTTP版本信息。  
* 请求首部字段。  
* 请求内容实体。  

响应报文：  
* 状态行，包括HTTP版本，状态码，状态码的原因短语。  
* 响应首部字段。  
* 响应内容实体。  



</p>
</details>  

***  

### 21.HTTP请求方式  
<details><summary><b></b></summary>
<p> 

#### 答案:   
* GET:请求访问已经被URI（统一资源标识符）识别的资源，可以通过URL，给服务器传递参数数据。  
* POST：传输信息给服务器，主要功能与GET方法类似，但传递的数据量通常不受限。   
* PUT:传输文件，报文主体包含文件内容，保存到对应URI的位置。   
* HEAD:获得报文首部，与get方法类似，只是不返回报文主体，一般用于验证URI是否有效。   
* DELETE：删除文件，与PUT方法相反，删除对应URL位置的文件。   
* OPTIONS:查询相应URI支持的HTTP方法。  

</p>
</details>  

***  

### 22.HTTP首部字段包括哪些类型  
<details><summary><b></b></summary>
<p> 

#### 答案:   
* 通用首部字段(请求报文和响应报文都会使用的首部字段)。  
> `Date`:创建报文的时间。  
> `Connection`:连接的管理。  
> `Cache-Control`:缓存机制。  
> `Transfer-Encoding`:报文主体的传输编码方式。  

* 请求首部字段（请求报文会使用的首部字段）。  
> `Host`: 请求资源所在的服务器。  
> `Accept`: 可处理的媒体类型。  
> `Accept-Charset`: 可接受的字符集。  
> `Accept-Encoding`: 可接受的内容编码。  
> `Accept-Language`: 可接受的自然语言。  

* 响应首部字段（响应报文会使用的字段）。  
> `Accept-Ranges`: 可接受的字节范围。  
> `Location`: 令客户端重新定向到的URL。  

* 实体首部字段（请求报文和响应报文的实体部分使用的首部字段）。  
> `Allow`: 资源可支持的HTTP方法。  
> `Content-Type`: 实体主体的类型。  
> `Content-Encoding`: 实体主体使用的编码方式。  
> `Content-Language`: 实体主体的自然语言。  
> `Content-Length`: 实体主体的字节数。 
> `Content-Range`: 实体主体的位置范围，一般用于发出部分请求时使用。  

</p>
</details>  

***

### 22.`GET`和`POST`的区别
<details><summary><b></b></summary>
<p> 

#### 答案:   
* `GET`一般用于获取/查询资源，应该时安全幂等（对于同一URL的多个请求应该返回同样的结果）的；而`POST`一般用于更新资源信息，会修改服务器上的资源信息。  
* `GET`请求的数据会附在URI之后（就是把数据放在HTTP协议头中）；`POST`把提交的数据放在HTTP的requset body中。  
* `GET`方式提交的数据最多时1024字节，这个限制取决于操作系统的支持；理论上讲`POST`是没有大小限制的。  
* 在ASP中，服务端获取`GET`请求参数用Requset.QueryString;获取`POST`的请求参数用Requset.Form。  
* `POST`比`GET`安全性更高：`GET`提交数据，用户名和密码将明文出现在URL上；登录页面有可能被浏览器缓存；其他人可以查看浏览器历史记录；还可能造成Cross-site request forgery攻击。

</p>
</details>  

***  
