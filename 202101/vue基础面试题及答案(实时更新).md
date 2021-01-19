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

### 6.v-if和v-show的区别

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

