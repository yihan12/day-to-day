### facebook分享h5分享图文注意点

1. 分享需要原生配合，一起实现分享功能。

2. 其次需要在index.html的头部配置meta如下内容

   ```javascript
   <meta property="og:site_name" content="site name"/>
   <meta property="og:title" content="title"/>
   <meta property="og:type" content="website"/>
   <meta property="og:description" content="description"/>
   <meta property="og:image" content="http://yourdomain.com/images/hatenablog.png"/>
   <meta property="og:url" content="http://yourdomain.com/test.html">
   ```

3.url中的content网址必须是标注网址，不能加任何参数。
