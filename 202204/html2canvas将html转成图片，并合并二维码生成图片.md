### 概述

目的

> 将周报页面生成图片，并且带上二维码，需要 h5 合成图。最后和原生配合将整体图片分享出去。

当前组成组件是方便后续需要分享的直接调用组件就能生成需要的分享图。这个组件仅支持携带二维码的分享图，且二维码是固定，如需新的二维码需要新增新二维码图，并对源码进行相应调整。

### 注意点

###### 1.html2canvas 首先将 html 生成图片，要注意需要将屏幕滚动到顶部，不然图片会被截断;然后再进行将 html 生成快照

```
document.body.scrollTop = document.getElementById("weekly").scrollTop = 0;
```

###### 2.如果按照当前比例生成图片，图片的清晰度会很差。需要生成两倍的图。

```
// 设置放大倍数
const scale = window.devicePixelRatio || 2;
```

###### 3.canvas 需要关闭抗锯齿

```
// 【重要】关闭抗锯齿
context.mozImageSmoothingEnabled = false;
context.webkitImageSmoothingEnabled = false;
context.msImageSmoothingEnabled = false;
context.imageSmoothingEnabled = false;
```

###### 4.多图绘制如果高度有小数，容易造成两图之间有白条。需要将绘制出来的高度绘制到 canvas 时，需要向下取整

```
// 初始化canvas
const canvas = document.createElement("canvas");
let context = canvas.getContext("2d");
canvas.width = scale * width;
canvas.height =
    scale * Math.floor(height) + (canvas.width / 375) * 74;
const imgsrcArray = [
    {
        imgUrl: res,
        l: 0,
        w: canvas.width,
        h: scale * Math.floor(height),
    },
    {
        imgUrl: shareCode,
        l: (canvas.width / 375) * 15, //左边距
        w: canvas.width - (canvas.width / 375) * 30, //宽度
        h: (canvas.width / 375) * 44,
    },
];
```

###### 5.给整个 canvas 用相同的背景色

```
// 绘制矩形添加背景色
context.rect(0, 0, canvas.width, canvas.height);
context.fillStyle = "#282A35"; // 整个canvas的背景色
```

###### 6.当前 html2canvas 版本是 1.3.3，高版本无法兼容生成的图片会出现部分白的 bug

### 使用

需要传入的元素

```
const data = reactive({
  // 包裹元素名称
  main: props.main,
  // 生成元素名称
  content: props.content,
  // #+生成元素名称
  contentId: props.contentId,
});
```

引入组件并传入需要生成 html 的 id

```
<template>
    <html-toimage
      :main="'contentMain'"
      :content="'contentM'"
      :contentId="'#contentM'"
    ></html-toimage>
    <div id="contentMain">
        <div id="contentM">
        </div>
    </div>
</template>

<script>
import HtmlToimage from "@/components/HtmlToimage/index.vue";
export default{
    components:{
        HtmlToimage
    }
}
</script>
```

### 源码

```
<template>
  <div class="share">
    <van-button @touchstart="toImage" :icon="shareImg" type="primary" />
  </div>
</template>

<script>
import userAgent from "@/utils/ua-parser";
const isApp = userAgent.isApp();
import html2canvas from "html2canvas";
import { reactive, ref } from "@vue/reactivity";
import btn_nav_share from "./btn_nav_share.svg";
import shareCode from "./weekly@2.png";
import { onMounted } from "@vue/runtime-core";
export default {
  props: {
    main: {
      type: String,
      default: "contentMain",
    },
    content: {
      type: String,
      default: "contentM",
    },
    contentId: {
      type: String,
      default: "#contentM",
    },
  },
  setup(props) {
    const data = reactive({
      // 包裹元素名称
      main: props.main,
      // 生成元素名称
      content: props.content,
      // #+生成元素名称
      contentId: props.contentId,
    });
    // 将html页面生成快照
    const convertToImage = (container, options = {}) => {
      // 设置放大倍数
      const scale = window.devicePixelRatio || 2;

      // 传入节点原始宽高
      const _width = container.offsetWidth;
      const _height = container.offsetHeight;

      let { width, height } = options;
      width = width || _width;
      height = height || _height;
      const ops = {
        scale,
        width,
        height: height,
        useCORS: true,
        allowTaint: false,
        ...options,
      };

      return html2canvas(container, ops).then((canvas) => {
        // 返回图片的二进制数据
        return canvas.toDataURL("image/png");
      });
    };

    onMounted(() => {});

    const toImage = () => {
      let weeklyCon = document.getElementById(data.content);
      // 当前页面的宽度
      const width = weeklyCon.offsetWidth;
      const height = weeklyCon.offsetHeight;
      const scale = window.devicePixelRatio || 2;
      // 设置放大倍数
      document.body.scrollTop = document.getElementById(
        data.main
      ).scrollTop = 0;

      convertToImage(document.querySelector(data.contentId), {
        width,
        height,
      }).then((res) => {
        // 初始化canvas
        const canvas = document.createElement("canvas");
        let context = canvas.getContext("2d");
        canvas.width = scale * width;
        canvas.height =
          scale * Math.floor(height) + Math.floor(canvas.width / 375) * 84;
        console.log(canvas.width, canvas.height, scale * 44);
        const imgsrcArray = [
          {
            imgUrl: res,
            l: 0,
            w: canvas.width,
            h: scale * Math.floor(height),
          },
          {
            imgUrl: shareCode,
            l: (canvas.width / 375) * 15, //左边距
            w: canvas.width - (canvas.width / 375) * 30, //宽度
            h: (canvas.width / 375) * 44,
          },
        ];

        // 绘制矩形添加背景色
        context.rect(0, 0, canvas.width, canvas.height);
        context.fillStyle = "#282A35"; // 整个canvas的背景色

        // 【重要】关闭抗锯齿
        context.mozImageSmoothingEnabled = false;
        context.webkitImageSmoothingEnabled = false;
        context.msImageSmoothingEnabled = false;
        context.imageSmoothingEnabled = false;
        context.fill();

        // 多图绘制，下一张的y应该是上一张的高度
        let beforeHeight = 0;
        let p = [];

        imgsrcArray.forEach((img) => {
          let p1 = new Promise((resolve) => {
            let myImage = new Image();
            //背景图片  你自己本地的图片或者在线图片
            myImage.src = img.imgUrl;
            // 防止跨域
            myImage.crossOrigin = "Anonymous";
            myImage.onload = function () {
              //将res数据画在canvas中的顶部（left：0，top：0）。宽度为canvas.width，高度为scale * height
              context.drawImage(myImage, img.l, beforeHeight, img.w, img.h);
              beforeHeight = beforeHeight + img.h;
              console.log(img.l, beforeHeight, img.w, img.h);
              resolve(true);
            };
          });
          p.push(p1);
        });

        Promise.all(p).then((res) => {
          try {
            console.log(res);
            const base64 = canvas.toDataURL("image/png"); //"image/png" 这里注意一下
            // 将base64数据的图片直接放到avatar中
            const img = document.getElementById("avatar");
            // document.getElementById('avatar').src = base64;
            img.setAttribute("src", base64);
            // shareWeekly(base64);
            if (isApp) {
              sendImageMessage(base64).then((data) => {
                console.log(data, "图片信息");
              });
            }
          } catch (e) {
            console.log(e);
          }
        });
      });
    };

    const shareImg = ref(null);
    shareImg.value = btn_nav_share;

    return { shareImg, toImage };
  },
};
</script>

<style lang="less" scoped>
.share {
  .van-button--normal {
    width: 100%;
    background: none;
    border: 0;
    font-size: 20px;
  }
}
</style>
```
