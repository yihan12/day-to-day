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


/*talkBottom*/
#talkBottom:before{
  content:" ";
  position:absolute;
  top:100%;
  left:50px;
  width:0;
  height:0;
  border-left:15px solid transparent;
  border-top:15px solid #808080;
  border-right:15px solid transparent;
}
#talkBottom:after{
  content:" ";
  position:absolute;
  top:100%;
  left:51px;
  width:0;
  height:0;
  border-left:14px solid transparent;
  border-top:14px solid #fff;
  border-right:14px solid transparent;
}
#talkBottom:hover{
  color:#fff;
  background-color:#ff0000;
}
#talkBottom:hover:after{
  width:0;
  height:0;
  border-left:14px solid transparent;
  border-top:14px solid #ff0000;
  border-right:14px solid transparent;
}

/*talkTop*/
#talkTop:before{
  content:" ";
  position:absolute;
  top:-15px;
  left:50px;
  width:0;
  height:0;
  border-left:15px solid transparent;
  border-bottom:15px solid #808080;
  border-right:15px solid transparent;
}
#talkTop:after{
  content:" ";
  position:absolute;
  top:-14px;
  left:51px;
  width:0;
  height:0;
  border-left:14px solid transparent;
  border-bottom:14px solid #fff;
  border-right:14px solid transparent;
}
#talkTop:hover{
  color:#fff;
  background-color:#ff0000;
}
#talkTop:hover:after{
  width:0;
  height:0;
  border-left:14px solid transparent;
  border-bottom:14px solid #ff0000;
  border-right:14px solid transparent;
}


/*talkLeft*/
#talkLeft:before{
  content:" ";
  position:absolute;
  top:15px;
  left:-7px;
  width:0;
  height:0;
  border-top:7px solid transparent;
  border-right:7px solid #808080;
  border-bottom:7px solid transparent;
}
#talkLeft:after{
  content:" ";
  position:absolute;
  top:16px;
  left:-6px;
  width:0;
  height:0;
  border-top:6px solid transparent;
  border-right:6px solid #fff;
  border-bottom:6px solid transparent;
}
#talkLeft:hover{
  color:#fff;
  background-color:#ff0000;
}
#talkLeft:hover:after{
  width:0;
  height:0;
  border-left:6px solid transparent;
  border-right:6px solid #ff0000;
  border-bottom:6px solid transparent;
}


/*talkRight*/
#talkRight:before{
  content:" ";
  position:absolute;
  top:15px;
  right:-7px;
  width:0;
  height:0;
  border-top:7px solid transparent;
  border-left:7px solid #808080;
  border-bottom:7px solid transparent;
}
#talkRight:after{
  content:" ";
  position:absolute;
  top:16px;
  right:-6px;
  width:0;
  height:0;
  border-top:6px solid transparent;
  border-left:6px solid #fff;
  border-bottom:6px solid transparent;
}
#talkRight:hover{
  color:#fff;
  background-color:#ff0000;
}
#talkRight:hover:after{
  width:0;
  height:0;
  border-left:6px solid transparent;
  border-left:6px solid #ff0000;
  border-bottom:6px solid transparent;
}
```
