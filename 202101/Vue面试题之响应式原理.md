### MVVM  

#### 什么是MVVM？ 
**MVVM**是Model-View-ViewModel,是把一个系统分为了模型（model）、视图（view）和view-model三个部分。vue是一个典型的MVVM思想，**数据驱动视图**。  
通俗一点就是**view层不直接和model层通信**，他们只能通过view-model层通信。

#### vue是怎么实现MVVM的？  
vue是一个MVVM渐进式框架，MVVM是vue的实际模式，在vue框架中数据会自动驱动视图。我们写vue就知道它的单文件组件开发方式。  
**Model**：数据层，仅仅关注数据本身，不关心任何行为。  

> 对应vue组件中的data，props属性。

**View**：视图层，用户操作页面，当view-model对model更新的时候，会通过数据绑定更新到view。  

> vue组件中的template和style的部分。  

**ViewModel**：业务逻辑层，view需要什么数据，ViewModel就提供什么数据，view有些哪些操作，ViewModel就要响应这些操作；View和ViewModel两种交互方式：双向数据传递（数据属性和data binding）和单向传递操作（命令属性）；由于ViewModel的双向数据绑定，当Model发生变化时，ViewModel就会更新，ViewModel变化，Model也会更新。  

> 继承Vue类的组件实例  

vue在MVVM
