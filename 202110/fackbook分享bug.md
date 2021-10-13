### facebook分享h5分享图文注意点

1. 我们的需求是原生配合，一起实现分享功能。

2. 其次需要在index.html的头部配置meta如下内容

   ```javascript
   <meta property="og:site_name" content="site name"/>
   <meta property="og:title" content="title"/>
   <meta property="og:type" content="website"/>
   <meta property="og:description" content="description"/>
   <meta property="og:image" content="http://yourdomain.com/images/hatenablog.png"/>
   <meta property="og:url" content="http://yourdomain.com/test.html">
   ```
    >  1.title fb可以自动读取要分享页面的title 这个要设置在fb的sharer.php参数里,你也可以自己设置 方式就是  
    >  <meta property="og:title" content="test" />   
    >  2.image标签 可以写多个 分享人可以自己选择图片   
    >  3.url就是你的要分享的页面   
    >  4.description 介绍信息   
   
3. url中的content网址必须是标注网址，不能加任何参数。  
   因此，分享页需要绑定用户不能直接通过一下形式  
   
   ```javascript
   https://www.your-domain.com/your-page.html?a=1

   https://www.your-domain.com/your-page.html?a=1&b=2
   ```
   
   解决方案：把参数写成路径形式  
   
   ```javascript
   https://www.your-domain.com/2/68/your-page.html
   ```
   
 4.图片像素必须是100*100 
