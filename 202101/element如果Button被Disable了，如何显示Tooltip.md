### 需求  
按钮被disabled了需要显示tooltip

### 错误案例  
直接用tooltip包着按钮  
```javascript
<el-tooltip placement="top" :disabled="tooltipDisabled" content="按钮被disabled了需要显示tooltip">
    <el-button style="margin-bottom:10px" :disabled="btnDisabled" type="primary" size="small" @click="handleEdit">上传脚本</el-button>
</el-tooltip>
```

### 解决  
> 在tooltip中可以用disabled来控制tooltip是否可用  
> 用div包着button；并且宽度设置与button大小一致（我这里使用的宽度是80px）  

代码如下：  
```javascript
<el-tooltip placement="top" :disabled="tooltipDis" content="脚本版本数不能超过5个，请删除弃用的脚本后再上传。">
  <div style="width:80px">
    <el-button style="margin-bottom:10px" :disabled="upLoadDisabled" type="primary" size="small" @click="handleEdit">上传脚本</el-button>
  </div>
</el-tooltip>
```
