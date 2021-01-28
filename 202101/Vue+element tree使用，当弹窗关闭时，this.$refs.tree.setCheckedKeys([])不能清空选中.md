### 问题

> Vue+element tree使用，当弹窗关闭时，`this.$refs.tree.setCheckedKeys([])`不能清空选中。 

### 解决

由于弹窗关闭，导致`this.$refs.tree.setCheckedKeys([])`无效。

此时，需要我们重新获取整个树组件的node，然后将对应的每个选项`checked`为空。

```javascript
// 首先获取node
let node = this.$refs.tree.getNode(this.data[0].id).parent;
// 这里的this.data是指的树的数据;而id是指，:node-key="id"这里的id。从而获取到整个树的node
// 然后便历树，将所有的checked改成false
node.childNodes.map(val=>{
  val.checked = false;
  if(val.childNodes&&val.childNodes.length>0){
    val.childNodes.map(value=>{
      value.checked = false
    })  
  }
})
```
