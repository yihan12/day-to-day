### 问题  

> chrome版本号89.0.4389.90，不支持less的`/deep/`样式穿透

### 解决  

既要照顾以前的版本，又要兼容新版本，建议写两种css样式 

```css
.main{
  .el-dialog__headerbtn{
      top:-5px!important;
      right:0px!important;
  }
  /deep/.el-dialog__headerbtn{
      top:-5px!important;
      right:0px!important;
  }
}
```

**注意：`/deep/`只适用less，sass用`::v-deep`**
**注意：`/deep/`的最好放在没`/deep/`的后面**  
