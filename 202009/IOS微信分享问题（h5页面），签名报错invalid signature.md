### 前言

网上方法差不多都看了，有个解决方法：window.location.href;确实有效，但是必须进入页面后再次刷新页面才能签名成功；用时间戳也不能解决刷新问题

### 方法

在mian.js里面全局路由守卫后置钩子afterEach，主动修改url

```javascript
window.router=router；
router.afterEach(to => {
  const u = navigator.userAgent.toLowerCase();
  if (
    u.indexOf("like mac os x") < 0 ||
    u.match(/MicroMessenger/i) != "micromessenger"
  )
    return;
  if (to.path !== global.location.pathname) {
    location.assign(to.fullPath);
  }
});
```

亲测window.location.href是有用但是需要再次刷新页面才会签名成功，！window.location.href刚跳转进去是不能签名成功的；改变全局路由守卫后置钩子就不需要改变push的切换页面方式，当它是ios端的时候会主动改变的url。还有window.location.href有个跳转效果不好，还会重新获取数据
