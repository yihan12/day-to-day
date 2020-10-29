### 问题

```javascript
yAxis: {
      type: 'category',
      data: yAxis,
      axisLabel: {
        inside: true,
        *verticalAlign: 'middle'*
        // 文档中应该是这个属性来设置垂直居中，但是未生效
      },
      axisLine: {
        lineStyle: {
          color: '#fff',
        },
      },
      zlevel: 1,
    },
```

### 解决

设置textStyle lineHeight

```javascript
axisLabel:{
       textStyle:{
          color: "#444",
          fontSize: 8,
          lineHeight: 9
       },
}
```
