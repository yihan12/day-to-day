### 问题

>图片加文字的无缝滚动，在手机端的效果总体还行，但是图片在手机某些浏览器会抖得腻害！

### 错误写法

不能用left，margin-left,像这种写法:

```css
.donghua.active{
  animation: scoll ease-in-out 1s infinite alternate;
  -webkit-animation: scoll ease-in-out 1s infinite alternate;
}
@keyframes scoll  {
  from {
    left: 0;
  }
  to {
    left: -353px;
  }
}
-webkit-@keyframes scoll  {
  from {
    left: 0;
  }
  to {
    left: -353px;
  }
}
```

### 方法

里面的某个元素在手机端会抖动的腻害,改用二维的translate像这样:

```css
.donghua.active{
  animation: scoll ease-in-out 1s infinite alternate;
  -webkit-animation: scoll ease-in-out 1s infinite alternate;
}
@keyframes scoll {
  0% {
    transform: translate(0px, 0px);
  }

  100% {
    transform: translate(0px, -353px);
  }
}
@-webkit-keyframes scoll {
  0% {
    transform: translate(0px, 0px);
  }

  100% {
    transform: translate(0px, -353px);
  }
}
```
