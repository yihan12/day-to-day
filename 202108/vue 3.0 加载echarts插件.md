### 首先在需要echarts页面引入echarts  

```javascript
import * as echarts from "echarts";
```

### template部分的内容

```javascript
<template>
<div id="mainBlance" style="width: 100%;height:260px; max-height: 400px;">
</template>
```

### export中定义echarts  

```javascript
import { onMounted, defineComponent } from "vue";
export default defineComponent({
  name: "Echarts",
  data() {
    return {
      value: 0,
      option: [
        { text: "年报", value: 0 },
        { text: "中报", value: 1 },
        { text: "一季报", value: 2 },
        { text: "三季报", value: 3 },
      ],
      numLi: [20, 18, 15, 10, 80],
      balanceLi: [30, 80, 15, 40, 90],
      sizeLi: [30, 57.1, 92.1, 50, 55.5],
    };
  },
  setup() {
    //methods
    const echartInit = () => {
      let myChart = echarts.init(document.getElementById("mainBlance"));
      // 指定图表的配置项和数据
      let option = {
        grid: {
          x: 0,
          y: 45,
          x2: 0,
          y2: 20,
          borderWidth: 1,
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "cross",
            crossStyle: {
              color: "#999",
            },
          },
        },
        toolbox: {},
        legend: {
          show: true,
          itemWidth: 6,
          itemHeight: 6,
          left: 0,
          top: 10,
          textStyle: {
            color: "#808080",
          },
          data: [
            {
              name: "每股净资产",
              // 强制设置图形为圆。
              icon: "rect",
              // 设置文本为红色
              // textStyle: {
              //   color: "#398FFE",
              // },
              itemStyle: {},
            },
            {
              name: "总负债（亿）",
              // 强制设置图形为圆。
              icon: "rect",
              // 设置文本为红色
              // textStyle: {
              //   color: "#398FFE",
              // },
              itemStyle: {},
            },
            {
              name: "同比增长率",
              // 强制设置图形为圆。
              icon: "circle",
              // 设置文本为红色
              // textStyle: {
              //   color: "#F5A200",
              // },
            },
          ],
        },
        xAxis: [
          {
            type: "category",
            data: ["2015/FY", "2016/FY", "2017/FY", "2018/FY", "2019/FY"],
            axisLabel: {
              show: true,
              interval: 0, // 坐标轴刻度标签的显示间隔
              textStyle: {
                color: "#808080",
                fontSize: 12,
              },
            },
            nameTextStyle: {
              color: "#808080",
              fontSize: 14,
            },
            axisTick: {
              show: false,
            },
            axisLine: {
              lineStyle: {
                color: "#EBEBEB",
              },
            },
          },
        ],
        yAxis: [
          {
            type: "value",
            // name: "每股净资产",
            min: 0,
            max: 100,
            interval: 20,
            splitLine: {
              show: true,
              lineStyle: {
                type: "dashed",
              },
            },
            axisLabel: {
              show: false,
            },
          },
          {
            type: "value",
            // name: "同比增长率",
            min: 0,
            max: 100,
            interval: 20,
            axisLabel: {
              show: false,
            },
            splitLine: {
              show: true,
              lineStyle: {
                type: "dashed",
              },
            },
          },
        ],
        series: [
          {
            name: "每股净资产",
            type: "bar",
            data: [20, 18, 15, 10, 80],
            /*设置柱状图颜色*/
            itemStyle: {
              color: "#398FFE",
            },
            barWidth: 12,
          },
          {
            name: "总负债（亿）",
            type: "bar",
            data: [30, 80, 15, 40, 90],
            /*设置柱状图颜色*/
            itemStyle: {
              color: "#B1D3FF",
            },
            barWidth: 12,
          },
          {
            name: "同比增长率",
            type: "line",
            yAxisIndex: 1,
            data: [30, 57.1, 92.1, 50, 55.5],
            itemStyle: {
              color: "#F5A200",
            },
            symbol: "circle",
            symbolSize: 6,
          },
        ],
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    };
    //onMounted
    onMounted(() => {
      echartInit();
    });
    //return
    return {
      echartInit,
    };
  },
});

```
