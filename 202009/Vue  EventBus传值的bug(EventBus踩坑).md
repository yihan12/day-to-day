
### 前言

>三个兄弟组件通信
>
>EventBus未取消绑定,重复触发的bug


### 基本使用

```javascript
/新建一个 js 文件，写下如下代码就创建好了一个 eventbus，没错，就是这么简单
import Vue from 'vue'

export default new Vue;
```

#### 全局调用

在 main.js 中导入 eventbus ，然后将它挂载到 vue 的原型上，这样就可以全局调用了

```javascript
import bus from './utils/eventBus'
Vue.prototype.bus = bus;
```

其他文件
```javascript
//发送
this.bus.$emit(this.$route.path);

//接收
this.bus.$on(this.$route.path,()=>{
  this.getData();
})

//销毁
beforeDestroy() {
  //组件销毁前需要解绑事件。否则会出现重复触发事件的问题
  this.bus.$off(this.$route.path);
},
```
#### 简单调用

```javascript
import bus from './utils/eventBus'

//发送
bus.$emit('get', {
  item: item.type,
  date: date
})

//接收
bus.$on('get', this.myhandle)

//销毁
beforeDestroy() {
  //组件销毁前需要解绑事件。否则会出现重复触发事件的问题
  bus.$off('get');
},
```

### 尤大大提出了以下解决
```javascript
// 在B组件页面中添加以下语句，在组件beforeDestory的时候销毁。
beforeDestroy () {
  bus.$off('get', this.myhandle)
},
```
如果想要用bus 来进行页面组件之间的数据传递，需要注意亮点，组件A$emit事件应在beforeDestory生命周期内。其次，组件B内的$on记得要销毁。

### 处理经验
1:虽然尤大大解决方案能销毁$on,但是多个eventbus,处理不慎,容易导致事件不能再次触发;

2:多个eventbus,多个组件实时交互,处理逻辑复杂;

3:弹窗还有其他逻辑交流,多功能组件不适合使用eventbus,需要利用vuex实时交互;

4:维护困难

5:除非非常简单逻辑,否则不建议使用eventbus
