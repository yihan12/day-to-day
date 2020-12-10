### 日常
日常遇到的，同id的两数组合并成一数组的问题

### 语法

```javascript
arr.reduce(function(prev,cur,index,arr){
...
}, init);
```

> arr 表示原数组；

> prev 表示上一次调用回调时的返回值，或者初始值 init;

> cur 表示当前正在处理的数组元素；

> index 表示当前正在处理的数组元素的索引，若提供 init 值，则索引为0，否则索引为1；

> init 表示初始值。

注意:其实常用的参数只有两个：prev 和 cur

### 根据id合并两个数组

```javascript
let arr1 = [{ id: 1, age: '14' },{ id: 2, age: '23' },{ id: 3, age: '33' }]
let arr2 = [{ id: 3, name: 'zhangsan' },{ id: 1, name: 'lisi' },{ id: 2, name: 'wangwu' }]
const list = arr2.reduce((prev, cur) => {
  const target = prev.find(e => e.id === cur.id);
  if (target) {
    Object.assign(target, cur);
  } else {
    prev.push(cur);
  }
  return prev;
}, arr1);
console.log(list)
```

### 根据id,taId合并两个数组

```javascript
let arr1 = [{ taId: 1, age: '14' },{ taId: 2, age: '23' },{ taId: 3, age: '33' }]
let arr2 = [{ id: 3, name: 'zhangsan' },{ id: 1, name: 'lisi' },{ id: 2, name: 'wangwu' }]
const list = arr2.reduce((prev, cur) => {
  const target = prev.find(e => e.taId === cur.id);
  if (target) {
    Object.assign(target, cur);
  } else {
    prev.push(cur);
  }
  return prev;
}, arr1);
console.log(list)
```
