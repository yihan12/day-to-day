### 需求

> 输入必须为数字，正整数；小于15，大于0；

### 解决

首先element-ui的input组件

```javascript
<el-input type="text" :maxLength="2" autocomplete="off" v-model="maxNum" placeholder="请输入<=15的正整数"></el-input>
```
利用onkeyup，对输入的进行更改

最终代码

```javascript
<el-input 
  onkeyup="value=value.replace(/[^0-9]/g,'');if(value>15){value=15};if(String(value)==='0'){value=1}"
  type="text" 
  :maxLength="2" 
  autocomplete="off" 
  v-model="maxNum" 
  placeholder="请输入<=15的正整数">
</el-input>
```
