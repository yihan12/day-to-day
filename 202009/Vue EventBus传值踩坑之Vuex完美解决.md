### 问题

>多个组件通信问题
>
>EventBus传值,频繁会导致接口重复调用

我以为eventBus是专门处理兄弟组件之间通信的，但是实际上，eventBus是专门处理同一个路由下的复杂组件之间通信的。
如果涉及夸路由的组件通信。可以考虑利用$route对象传参或者Vuex

### vuex完美解决

由于涉及v-model,需要特殊处理:

bug
>computed property "XXX" was assigned to but it has no setter

store下的common.js
```javascript

```
