## 前言  
面试前的临时抱佛脚，也能系统的梳理下所掌握的知识。  

## 面试题

### 1.vue的生命周期，生命周期的理解。

<details><summary><b></b></summary>
<p>

#### 答案:   

> **创建**=>**挂载**=>**更新**=>**销毁**（也就是我们常说的**八个阶段**：`创建前/后`，`挂载前/后`，`更新前/后`，`销毁前/后`）。
> 
> 含义：Vue实例从创建到销毁的过程，就是生命周期。从开始创建、初始化数据、编译模板、挂载Dom===>渲染、更新===>渲染销毁等一系列过程，称之为Vue的生命周期。
> 
> 作用：Vue的生命周期有多个事件钩子，让我们在控制整个Vue实例的过程时更容易形成好的逻辑。
> 
> 第一次页面加载会触发的钩子函数：`beforeCreate`、`created`、`beforeMount`、`mounted`。
>
> Dom渲染在哪个周期就已经完成：`mounted`。
> 
> Vue的页面请求一般放在哪个生命周期：`created`和`mounted`（区别：mounted周期中Dom已经渲染完成，再去请求数据，就会有空壳Dom的情况，会影响布局；而created周期中操作Dom节点会找不到Dom）。

如下图（vue生命周期官网）：  
![vue生命周期](https://cn.vuejs.org/images/lifecycle.png)  

上图理解：  
首先需要我们去执行一个实例`new Vue()`，首先执行了init(init是vue组件默认去执行的)，这时是事件和生命钩子的初始化（`Init Events&Lifecycle`）;  
在实例初始化之后（`Init Events&Lifecycle`）调用了beforeCreate,此时事件已经好了，也能开始生命周期了（读取配置项，加载生命周期的方法）。  
> **说明：这个时候this不能使用，data中的数据、methods的方法，以及watcher中的事件都不能获得**；  

接着初始化inject、provide、state属性（设置data、methods、computed...等配置项），也就是`Init injections(注射)&reactivity(反应性)`。在实例调用完成后他会立即调用created。在这一步，实例已经完成以下配置：数据观测（data observer）、属性和方法的运算、watch/event事件回调；然而挂载阶段还没开始，$el属性目前不可见。所以在init的时候，事件已经调用了，因此在beforeCreate的时候不要修改data里面赋值的数据，最早也要在created里面做（添加一些行为）。  
> **说明：created这个时候可以操作vue中的数据和方法，但是还不能对dom节点进行操作**  

当created完成之后，它会去判断，instance（实例）里面是否含有el对象`has 'el' option`。如果没有的话，它就会挂载`when vm.$mounted(el) is called`,然后走下一步，判断是否有模板`has 'template' option`;如果有的话，他就会直接跳到下一步，判断是否有模板`has 'template' option`。  
如果有模板'template'，就会把template解析成一个render function。通过render函数去渲染创建Dom树`compile template into render function`；如果没有模板'template'，就编译el对象外层html作为模板`compile el's outerHtml as template`。  
beforeMount再有了render函数的时候才会执行，此时$el和data都初始化了，但是在挂载前为虚拟的Dom节点。  
> **说明：$el属性已经存在，是虚拟Dom，只是数据未挂载到模板中**  

然后继续执行render函数，当执行完render函数之后，也就是el被新创建的vm.$el替换`Create vm.$el and replace 'el' with it`，并且挂载到实例上去之后就会调用mounted这个钩子。  
在mounted挂载完成，dom树已经完成渲染到页面，可进行dom操作。但是它不会承诺所有的子组件也都一起被挂载，如果希望等到整个视图都渲染完毕，可以用vm.$nextTick()。  
> **说明：挂载完毕，这时Dom节点被渲染到文档内，dom操作在此时能正常进行**   

当数据有更新，就会调用beforeUpdate，然后虚拟dom重新渲染补丁，以最小dom开支来重新渲染dom`Virtual Dom re-render and patch`。  
> **说明：beforeUpdate是指view层的数据变化前，不是data中数据改变前触发，因为Vue是数据驱动的。这里适合在更新之前访问现有Dom，比如手动移除已添加的事件监听器**  

然后就是updated执行。由于数据更改导致的虚拟Dom重新渲染和打补丁，在这之后会调用该钩子。当该钩子被调用时，组件Dom已经更新，所以你现在可以执行依赖于DOM的操作。然而在大多数情况，应该避免在此期间更改状态。如果要更改相应状态，最好使用计算属性或watcher取而代之。  
> **注意：updated不会承诺所有的子组件也都会被重构。如果你希望整个视图都重绘完毕，可以用vm.$nectTick()替换掉uopdated**  
> **说明： view层的数据更新后，data中的数据通beforeUpdate，都是更新完以后的。**  

beforeDestroy：实例在销毁之前调用，在这还能访问实例的数据`when vm.$destory() is called`。  
当组件销毁时，beforeDestroy执行，清除watcher、子组件、事件监听器等`Teardown watchers,child components and event listeners`。  
> **说明：实例在组件销毁之前调用，在这一步，实例完全可用**  

destroyed：Vue实例销毁后调用，调用后，Vue实例指示的所有东西会解绑，所有事件监听器会被移除，所有子实例也会被销毁。  
> **说明：执行destroy方法后，对data改变不会触发周期函数，此时，Vue实例已经解除事件监听和dom绑定，但是Dom结构依然存在**
</p>
</details>  

***

### 2.MVVM和MVC的区别

<details><summary><b></b></summary>
<p>

#### 答案:   
mvc和mvvm其实区别并不大，都是一种设计思想。主要是mvc的controller演变成mvvm的viewModel。mvvm主要解决了mvc中的大量的Dom操作是页面的渲染性能降低，加载速度变慢，影响用户体验。和当model频繁发生变化，开发者需要主动更新到view。
</p>
</details> 

***

### 3.vue的优点是什么

<details><summary><b></b></summary>
<p>

#### 答案:   
* 1.低耦合：视图`View`可以独立`Model`变化和修改，一个`ViewModel`可以绑定到不同的`View`上，当`View`变化的时候`Model`可以不变，当`Model`变化的时候`View`也可以不变。  
* 2.可重用性：可以把一些视图逻辑放在一个`ViewModel`里面，让很多`View`重用这段视图逻辑。  
* 3.独立开发：开发人员可以专注于业务逻辑和数据开发`ViewModel`,设计人员可以专注于页面设计，使用Expression Blend可以容易设计界面并生成xml代码。  
* 4.可测试：界面素来是比较难于测试的，而现在测试可以针对`ViewModel`来写。  
</p>
</details> 

***

### 4.vue组件间的参数传递

<details><summary><b></b></summary>
<p>

#### 答案:   
* 父组件与子组件传值：  
> 父组件传给子组件：子组件通过`props`方法接收数据；  
> 子组件传给父组件：`$emit`方法传递。  

* 兄弟组件间传值：  
> `eventBus`：就是创建一个实践中心，相当于中转站，可以用它来传递事件和接收事件；  
> `vuex`：适合比较大项目，具体看需求。  
</p>
</details> 

***

### 5.vue路由的实现：Hash模式和History模式

<details><summary><b></b></summary>
<p>

#### 答案:   
* **Hash模式**：是一种把前路由的路径用井号#拼接在真实URL后面的模式。当#后面的路径发生变化时，浏览器不会重新发起请求，而是会触发`haschange`事件。  
特点：hash虽然在URL中，但是不被包括在HTTP请求中；用来指导浏览器动作，对服务端的安全无用，hash不会重加载页面。  
优点：浏览器的兼容性比较好，支持IE8。  
缺点：路径在井号#后面，比较丑。  
读取：`window.location.hash`。  

* **History模式**：history采用HTML5的新特性；且提供两个方法：`pushState()`,`replaceState()`可以对浏览器历史记录栈进行修改，以及`popState`事件监听到状态变更。  
监听popState事件，该事件能监听到：用户点击浏览器前进后退的动作；手动调用history的`back`,`forward`和`go`方法。不能监听到：history的`pushState()`、`replaceState()`。  
优点：理解比较正规，没有井号。  
缺点：兼容性不如hash，且需要服务器支持，否则一刷新就404了。  
</p>
</details> 

***

### 6.vue路由跳转

<details><summary><b></b></summary>
<p>

#### 答案:   
声明式（标签跳转）  
```javascript
<router-link :to="index></router-link>
```

编程式（js跳转）  
```javascript
router.push('index')
```
</p>
</details> 

***

### 7.v-if和v-show的区别

<details><summary><b></b></summary>
<p>

#### 答案:   
* `v-if`：用于条件性渲染一块内容，这块内容只会在指令表达式返回`true`的时候被渲染。
* `v-show`：`v-show`的元素始终会被渲染保留在DOM中。`v-show`只是简单的切换元素css的display。  

区别：  
1.`v-show`是css显隐切换，v-if是完整的销毁和重新创建;  
2.使用频繁切换的时候用`v-show`，运行较少改变时用`v-if`;  
3.`v-if`是条件渲染，当false的时候不会渲染，页面也不会有html标签生成，`v-show`则是不管为true或者false，html元素都存在，只是css样式display的显隐;  
4.当我们需要经常切换某个元素的显隐时，使用`v-show`更加节省性能，当只需要一次切换时，使用`v-if`更加合理。  
</p>
</details> 

***

### 8.computed和watch的区别

<details><summary><b></b></summary>
<p>

#### 答案:   
* `computed`：  

> `computed`是计算属性，也就是计算值，更多用于计算值的场景;    
> 具有缓存性，`computed`的值在`getter`执行后是会缓存的，只有在它依赖的属性值改变之后，下一次获取`computed`的值时重新调用对应的`getter`来计算;   
> `computed`更适用于比较消耗性能的场景。  

* `watch`：  

> `watch`更多的是[观察]的作用，类似某些数据的监听回调，用于观察props和$emit或者本组件的值，当数据变化时来执行回调进行后续操作;  
> 无缓存性，页面重新渲染时值不变化也会执行。  

小结：  

> 当需要进行数值计算时，而且依赖于其他数据，可以把这个数据设计为`computed`;  
> 当需要在某个数据变化做一些事情，使用`watch`来观察这个数据的变化。

</p>
</details> 

***  

### 9.keep-alive组件的作用

<details><summary><b></b></summary>
<p>

#### 答案:   
`<keep-alive></keep-alive>`包裹动态组件时，会缓存不活动的组件实例，主要用于保留组件状态或避免重复渲染。  
> 比如有一个列表和一个详情，那么用户就会经常执行打开详情=>返回列表=>打开详情...这样的话列表和详情就会是一个很高频率打开的页面，那么对列表组件使用`<keep-alive></keep-alive>`进行缓存，这样用户每次返回列表的时候，都能从缓存中快速渲染，而不是重新渲染。
</p>
</details> 

***  

### 10.Vue组件的data为什么必须是函数

<details><summary><b></b></summary>
<p>

#### 答案:   
> vue组件的data值不能为对象，因为对象时引用类型，组件可能会被多个实例引用；  
> 如果data值是对象，将导致多个实例共享一个对象，其中一个组件改变data的属性值，其他实例也会受到影响。
</p>
</details> 

***  


### 11.Vue.nextTick和vm.$nextTick的作用

<details><summary><b></b></summary>
<p>

#### 答案:   
**官方**：  
> 在下次DOM更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的DOM。

Vue在更新DOM时时异步的，当数据发生变化时，Vue将开启一个一步更新的队列，视图需要等队列的所有数据变化完成之后，再统一进行更新；  

如果我们一直在修改相同的数据，异步操作队列还会去重；  

等待同一事件循环的所有数据变化完成之后，会将队列中的事件拿来进行处理，进行Dom更新。  

如果想在修改数据后立刻得到更新后的DOM结构，可以使用`Vue.nextTick()`

</p>
</details> 

***  

### 12.Vue指令有哪些，作用

<details><summary><b></b></summary>
<p>

#### 答案:   
* `v-if`:条件渲染指令。用于条件渲染一块内容，这块内容只能只在表达式返回`true`时才会被渲染。  
  `v-show`渲染的元素会始终保留在DOM中，`v-show`的切换只是`display`的显隐。  
* `v-for`：列表渲染指令。基于数组渲染一个列表。  
* `v-bind`：属性绑定指令。给标签属性赋值。    
  `v-text`：属性绑定指令。显示原文本。  
  `v-html`：属性绑定指令。以标签内容显示。  
* `v-on`：事件绑定指令。用来监听DOM事件，并在触发时运行一些js代码。  
  `v-on:click`、  
  `v-on:keydown`、  
  `v-on:mouseover`。  
* `v-model`：双向数据绑定指令。给value赋值。  
</p>
</details> 

***  

### 13.vue和react的区别

<details><summary><b></b></summary>
<p>

#### 答案:   

</p>
</details> 

***

### 13.vuex总结
<details><summary><b></b></summary>
<p>

#### 答案:   
vuex是一种状态管理机制，将全局组件的共享状态抽取出来为一个`store`,以一个单例的模式存在，应用任何一个组件中都可以使用，vuex更改`state`的唯一途径是通过`mutation`,`mutation`需要`commit`触发，`action`实际触发是`mutation`,其中`mutation`处理同步任务，`action`处理异步任务。
</p>
</details> 

***  

### 14.SPA单页面理解，优缺点？
<details><summary><b></b></summary>
<p>

#### 答案:   
> SPA(single-page application)仅在Web页面初始化时加载响应的HTML、JavaScript和CSS。一旦页面加载完成，SPA不会因为用户的操作而进行页面的重新加载或跳转；取而代之的是利用路由机制实现HTML内容的变换，UI与用户的交互，避免页面重新加载。  

优点：  
* 用户体验好，快，内容改变不需要重新加载整个页面，避免不必要的跳转和重复渲染；  
* SPA相对服务器压力小；  
* 前后端职责分离，架构清晰，前端进行交互逻辑，后端负责数据处理；  

缺点：  
* 首屏（初次）加载慢：为实现单页web应用功能及显示效果，需要在加载页面的时候将JavaScript、CSS统一加载，部分页面按需加载；  
* 不利于SEO：由于所有的内容在一个页面动态替换显示，所以在SEO上有着天然的弱势。
</p>
</details> 

***  

### 15.`new Vue()`发生了什么？
<details><summary><b></b></summary>
<p>

#### 答案:   
* `new Vue()`创建Vue实例，它内部执行了根实例的初始化过程。  
* 具体包括以下操作：  
    选项合并  
    `$children`、`$refs`、`$slots`、`$createElement`等实例的方法初始化  
    自定义时间处理   
    数据响应式处理  
    生命钩子的调用（beforecreate created）  
    可能的挂载  
* 总结：`new Vue()`创建了根实例并准备好数据和方法，未来执行挂载时，此过程还会递归的应用于它的子组件上，最终形成一个有紧密关系的组件实例树。  

</p>
</details> 

***  

### 15.vue性能优化
<details><summary><b></b></summary>
<p>

#### 答案:   
1） 编码阶段：  
* 尽量减少data中的数据，data中的数据都会增加getter和setter，会收集对应的watcher；  
* 如果需要使用v-for给每项元素绑定事件时使用事件代理；  
* SPA页面采用keep-alive缓存组件；  
* 在更多情况下使用v-if替代v-show；  
* key保证唯一；  
* 使用路由懒加载、异步组件；  
* 防抖节流；  
* 第三方模块按需导入；  
* 长列表滚动到可视区动态加载；  
* 图片懒加载、不在HTML里缩放图像、使用雪碧图（CSS sprite）、使用字体图标（iconfont）、使用WebP；
* 降低重绘重排的频率和成本；  
* CSS读写分离，不用js操作元素样式；  

2) 用户体验：  
* 骨架屏；  
* PWA；  
* 使用缓存（客户端缓存，服务端缓存，服务端开启gzip压缩）；  

3）SEO优化：  
* 预渲染；  
* 服务端渲染SSR；  

4）打包优化：  
* 压缩代码（注意：不要对图片文件进行Gzip压缩）；
* Tree Shaking/Scope Hoisting；  
* 使用cdn加载第三方模块；  
* 多线程打包happypack；  
* splitChunks抽离公共组件；  
* sourceaMap优化
</p>
</details> 

***  

### 16.vue首屏优化
<details><summary><b></b></summary>
<p>

#### 答案:   

</p>
</details> 

***  
