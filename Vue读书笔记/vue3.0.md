# vue3.0

#### 优势：

* vue3支持vue2大多数特性
* 更好的支持Typescript
* 性能提升：
  * 打包大小减少41%
  * 初次渲染快55%，更新渲染快133%
  * 内存减少54%
  * 使用Proxy代替Object.defineProperty实现数据响应式
  * 重写虚拟DOM的实现和Tree-Shaking
  
* 新增特性：
  * Composition（组合）API
  * setup(ref和reactive、computed和watch、新的生命周期函数、provide和inject、...)

* 新组件：
  * Fragment-文档碎片
  * Teleport-瞬移组件位置
  * Suspense-异步加载组件loading界面


* 其他API更新
  * 全局api修改
  * 将原来的全局api转移到应用对象
  * 模板语法变化
  



#### setup函数

> 在程序执行的时候，只执行一次

* 新的option，所有API函数都在此使用，只在初始化执行一次
* 函数如果返回对象，对象中的属性和方法，模板中可以直接使用



#### setup的细节

* **setup执行的时机**

  * 在`beforeCreate`之前执行一次，此时组件对象还没有创建
  * `this`是`undefined`，说明不能通过`this`调用`data/computed/methods/props`中的相关内容
  * 其实所有的composition API相关的回调函数也都不可以使用

* **setup返回值**

  * 一般都返回一个对象：为模板提供数据，也就是模板中可以直接使用该对象中的属性和方法
  * 返回对象中的属性会与data函数返回对象的属性合并成为组件对象的属性，也就是setup对象中的属性和data中return对象的属性都可以在html模板中使用
  * 返回对象的方法会与methods的方法合并成组件对象的方法
  * 如有重名，setup优先
  * 注意：
    * 一般不要混合使用：methods中可以访问setup提供的属性和方法，但在setup中不能访问data和methods
    * setup不能是一个async函数：以为返回值不再是return的对象，而是Promise，html模板看不到return对象中的属性数据

* ##### setup参数

  * `setup(props,context)`/`setup(props,{attrs,slots,emit,expose})`
    * `props`:是一个对象，包含props配置声明传入了所有属性的对象；里面有父级组件向自己组件传递的数据，并且是在自己组件中使用props接收到的所有属性。
    * `attrs`:包含没有在props配置声明的属性的对象，相当于`this.$attrs`
    * `slots`:包含所有传入插槽内容的对象，相当于`this.$slots`
    * `emit`:用来分发自定义事件的函数，相当于`this.$emit`



#### ref

* 作用：定义一个数据的响应式
* 语法：`const count = ref(0)`
  * 创建一个包含响应式数据的引用（reference）对象
  * js中操作数据`count.value`
  * 模板中操作数据，不需要`.value`

* 一般用来定义一个基本类型的响应式数据



#### reactive

> 返回的是一个Proxy的代理对象，被代理的目标就是reactive中的对象；
>
> 直接使用目标对象是不能更新视图数据；
>
> 只能使用代理对象的方式来更新数据（响应式数据）。

* 作用：定义多个数据的响应式
* `const proxy = reactive(obj)`：接收一个普通对象，然后返回该对象的响应式代理器对象。
* 响应式转换是深层的：会影响对象内部所有嵌套的属性。
* 内部基于ES6的Proxy实现，通过代理对象操作源对象的数据都是响应式的。

**总结：如果操作代理对象，目标对象中的数据也会随之变化；同时如果想要在操作数据的时候，界面也要跟着更新渲染，那么也是操作代理对象。**



#### reactive和ref细节

​	* 



#### 比较vue2和vue3的响应式

##### vue2的响应式

* 核心：
  * 对象：通过defineProperty对对象已有属性值的读取和修改进行劫持（监视/拦截）。
  * 数组：通过重写数组更新数组一系列更新的方法来实现元素修改的劫持。
* 问题：
  * 对象直接新添加的属性或删除已有属性，界面不会更新
  * 直接通过下标替换元素或更新length，界面不会自动更新

##### vue3的响应式

* 核心：

  * 通过Proxy（代理）：拦截对data任意属性的任意（13种）操作，包括属性值的读写，属性的添加，属性的删除等...
  * 通过Reflect（反射）：动态对被代理的对象的相应属性进行特定的操作。

  



