object-fit: fill; 
object-fit: contain; 
object-fit: cover; 
object-fit: none; 
object-fit: scale-down; 


object-position要比object-fit单纯的多，就是控制图片在盒子中显示位置的。默认值是50% 50%，也就是居中效果，所以，无论上一节object-fit值为那般，图片都是水平垂直居中的。因此，下次要实现尺寸大小不固定图片的垂直居中效果，可以试试object-fit.
与background-position类似，object-position的值类型为<position>类型值。也就是说，CSS3的相对坐标设定样式支持的。


注：目前IE应该还不支持object-fit和object-position属性



https://www.zhangxinxu.com/wordpress/2015/03/css3-object-position-object-fit/
https://www.cnblogs.com/libo0125ok/p/8422617.html
