### MVVM  

#### 什么是MVVM？ 
**MVVM**是Model-View-ViewModel,是把一个系统分为了模型（model）、视图（view）和view-model三个部分。vue是一个典型的MVVM思想，**数据驱动视图**。  
通俗一点就是**view层不直接和model层通信**，他们只能通过view-model层通信。

#### vue中MVVM的理解  
vue是一个MVVM渐进式框架，MVVM是vue的实际模式，在vue框架中数据会自动驱动视图。我们写vue就知道它的单文件组件开发方式。  
**Model**：数据层，仅仅关注数据本身，不关心任何行为。  

> 对应vue组件中的data，props属性。

**View**：视图层，用户操作页面，当view-model对model更新的时候，会通过数据绑定更新到view。  

> 对应vue组件中的template和style的部分。  

**ViewModel**：业务逻辑层，view需要什么数据，ViewModel就提供什么数据，view有些哪些操作，ViewModel就要响应这些操作；View和ViewModel两种交互方式：双向数据传递（数据属性和data binding）和单向传递操作（命令属性）；由于ViewModel的双向数据绑定，当Model发生变化时，ViewModel就会更新，ViewModel变化，Model也会更新。  

> 对应继承Vue类的组件实例  

vue在MVVM思想下，view和model没有直接联系，但是view和view-model、model和view-model之间是会交互的。当view视图进行dom操作等使数据发生变化时，可以通过view-model同步到model中，同样的model数据变化也会同步到vue中。  

#### MVVM的数据绑定实现  

* 发布者-订阅模式（backbone.js）  
* 脏值模式（angular/react）  
* 数据劫持（vue）  

### Vue实现MVVM的双向绑定

#### vue数据劫持结合发布者-订阅者模式 
vue是采用**数据劫持结合发布者-订阅者模式**的方式，通过`Object.defineProperty()`来劫持（监听）各个属性的`setter`，`getter`，在数据（对象）发生变动时发布消息给订阅者，触发相应的监听回调。  
因此，要实现MVVM的双向绑定就必须要实现以下几点：  
* 实现一个数据监听器Observer。对数据对象的所有属性进行监听（包括子属性对象的属性），利用`Object.defineProperty()`对属性都加上`setter`和`getter`（这样的话，给这个属性的某个值赋值就会触发 `setter`,那么就能监听数据的变化），如发生变动可拿到最新值并通知订阅者。  
* 实现一个指令解析器Compile。对vue每个元素节点的指令进行扫描和解析，将指令模板的变量都替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据发生变动，收到通知，调用更新函数进行数据更新。  
* 实现一个订阅者Watcher。Watcher是Observer和Compile之间通信的桥梁，主要任务是订阅Observer中的属性值变化的消息，当属性值发生变化时，触发解析器Compile中对应的更新函数，从而更新视图。  
* 实现MVVM入口函数，整合以上三者。
