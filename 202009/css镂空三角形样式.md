### 前言

>对话框----镂空三角形样式

### 原理

1)利用伪元素 :before :after

2):before ,border做出大三角形样式

3):after,border做出小三角形样式

4)小三角形的白色样式遮住大三角形样式,形成镂空

### 镂空三角形

html

```html
<div id="talkTop">
  顶部镂空三角形
</div>
<div id="talkBottom">
  底部镂空三角形
</div>
<div id="talkLeft">
  左边镂空三角形
</div>
<div id="talkRight">
  右边镂空三角形
</div>
```

css样式

```css
#talkTop,
#talkBottom,
#talkLeft,
#talkRight{
  width:120px;
  height:40px;
  margin:60px;
  line-height:40px;
  text-aligin:center;
  position:relative;
  -moz-border-radius:10px;
  -webkit-border-radius:10px;
  border-radius:10px;
  border-radius:1px solid #808080;
  background-color:#fff;
}
```
