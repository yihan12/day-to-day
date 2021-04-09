主要是利用css  
```css
max-width:min-content
```

如下代码展示  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .box{
      width: 100px;
    }
    .boxMain{
      display: flex;
      justify-content: space-between;
      padding: 2px 8px;
      border: 1px solid #ccc;
      background-color: aqua;
      overflow: hidden;
      color: #fff;
      width: 100%;
      max-width: min-content;
    }
    .l{
      max-width: min-content;
      /* 溢出用省略号显示 */
      text-overflow: ellipsis;
      overflow: hidden;
      /* 溢出不换行 */
      white-space: nowrap;
    }
  </style>
</head>
<body>
    <div class="box">
      <div class="boxMain">
        <div class="l">css自适应样式max-width:min-content</div>
        <div class="r">>>></div>
      </div>
    </div>
  
</body>
</html>
```

更改.box的width大小，便可看到内部会随宽度的增大减小而变化
