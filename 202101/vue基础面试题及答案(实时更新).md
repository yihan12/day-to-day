## 前言  
面试前的临时抱佛脚，也能系统的梳理下所掌握的知识。  

## 面试题

### 1.vue的生命周期，生命周期的理解。

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
在实例初始化之后（`Init Events&Lifecycle`）调用了beforeCreate,此时事件已经好了，也能开始生命周期了（读取配置项，加载生命周期的方法）。**说明：这个时候this不能使用，data中的数据、methods的方法，以及watcher中的事件都不能获得**；  
接着初始化inject、provide、state属性（设置data、methods、computed...等配置项），也就是`Init injections(注射)&reactivity(反应性)`。在实例调用完成后他会立即调用created。  



