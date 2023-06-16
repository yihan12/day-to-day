### 问题描述
> Echarts重新加载数据但不重新渲染的原因,主要出现在ios手机上。集体表现：第一次进入页面会出现，当第二次进入页面后，echarts部分就不会展示。

主要原因：如果echarts未实例化则进行实例化过程,一旦实例化，便会在div容器生成一个 echarts_instance 属性, 该属性值即为当前echarts的ID,然后根据该ID进行渲染。

### 解决

#### 方法一

```javascript
document.getElementById('ActionFinishEcharts').setAttribute('_echarts_instance_','')
myChart.setOption(option,true);
```

#### 方法二

```javascript
let a = document.getElementById("ActionFinishEcharts")
a.removeAttribute('_echarts_instance_')
myChart = echarts.init(a);
```
