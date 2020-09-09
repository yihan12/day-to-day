### 主要原因

X轴文字太多,需要文字倾斜角度,换行以及省略

### X轴文字倾斜角度,换行
interval

>坐标轴刻度标签的显示间隔(在类目轴中有效哦)，默认会采用标签不重叠的方式显示标签（也就是默认会将部分文字显示不全）可以设置为0强制显示所有标签，如果设置为1，表示隔一个标签显示一个标签，如果为3，表示隔3个标签显示一个标签，以此类推

rotate

>标签倾斜的角度，在类目轴的类目标签显示不全时可以通过旋转防止标签重叠（官方这样说的）旋转的角度是-90到90度

```javascript
xAxis:{
  axisLabel:{
    interval: 0,//X轴信息全部展示
    rotate: -60,//60 标签倾斜的角度
  }
}
```

### 依旧受到遮挡

这个名称x轴的文字如果太长会受到遮挡，还是显示不全，这个时候可以用grid属性解决

```javascript
grid: {
  left: '10%',
  bottom:'35%'
},
```

### 需求(中文显示两行,文字过多显示省略号;长日期显示一行,过多显示省略号)
formatter

>axisLabel中使用formatter回调，formatter有两个参数，使用方法是这样的formatter:function(value,index){} ，value是类目（测试医院A，人民医院）,index 是类目索引。

```javascript
xAxis:{
  axisLabel:{
     formatter:function(value){
        let ret = ""; //拼接加\n返回的类目项
        let maxLength = 8; //每项显示文字个数
        if(value.length>2*maxLength){
          value = value.substring(0, 2*maxLength - 3) + "...";
        }
        let valLength = value.length; //X轴类目项的文字个数
        let rowN = Math.ceil(valLength / maxLength); //类目项需要换行的行数
        if(/.*[/u4e00-/u9fa5]+.*$/.test(value)){//判断是否有中文
          if(rowN > 1){
            for (let i = 0; i < rowN; i++) {
                let temp = "";//每次截取的字符串
                let start = i * maxLength;//开始截取的位置
                let end = start + maxLength;//结束截取的位置
                //这里也可以加一个是否是最后一行的判断，但是不加也没有影响，那就不加吧
                temp = value.substring(start, end) + "\n";
                ret += temp; //凭借最终的字符串
            }
            return ret
          }else{
            return value 
          }
        }else{
          return value
        }
     }
  }
}
```

### 总结

整体代码

```javascript
op1:{
  grid: {
    left: '10%',
    bottom:'35%'
  },
  xAxis:{
    axisLabel:{
       textStyle:{
          color: "#444",
          fontSize: 8,
          lineHeight: 9
       },
       formatter:function(value){
          let ret = ""; //拼接加\n返回的类目项
          let maxLength = 8; //每项显示文字个数
          if(value.length>2*maxLength){
            value = value.substring(0, 2*maxLength - 3) + "...";
          }
          let valLength = value.length; //X轴类目项的文字个数
          let rowN = Math.ceil(valLength / maxLength); //类目项需要换行的行数
          if(/.*[/u4e00-/u9fa5]+.*$/.test(value)){//判断是否有中文
            if(rowN > 1){
              for (let i = 0; i < rowN; i++) {
                  let temp = "";//每次截取的字符串
                  let start = i * maxLength;//开始截取的位置
                  let end = start + maxLength;//结束截取的位置
                  //这里也可以加一个是否是最后一行的判断，但是不加也没有影响，那就不加吧
                  temp = value.substring(start, end) + "\n";
                  ret += temp; //凭借最终的字符串
              }
              return ret
            }else{
              return value 
            }
          }else{
            return value
          }
       }
    },
    interval: 0,//X轴信息全部展示
    rotate: -60,//60 标签倾斜的角度
  }
}
```
