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

