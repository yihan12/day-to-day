### 问题

> vue+element 列表

>后台数据更新了,console.log 打印出来是更新的

>但列表前端视图未改变

### 解决

```javascript
this.$set(this.data,key,value)
```

set函数接收三个参数分别为 target、key、val，其中target的值为数组或者对象，这正好和官网给出的调用Vue.set()方法时传入的参数参数对应上。

```javascript
Vue.set(target,propertyName/index,value)

this.$set(target,propertyName/index,value)
```

参数：

```javascript
{Object | Array} target
{string | number} propertyName/index
{any} value
```

返回值：设置的值。

用法：

向响应式对象中添加一个 property，并确保这个新 property 同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新 property，因为 Vue 无法探测普通的新增 property (比如 this.myObject.newProperty = 'hi')

