### 问题

>ios调用微信扫一扫scanQRCode报错the permission value is offline verifying

```javascript
document.getElementById("scanQRCode").onclick = function() {
  wx.scanQRCode({
    needResult: 1, // 默认为0，扫描结果由微信处理，1则直接返回扫描结果
    success: function(res) {
      alert("234");
      let data = res.resultStr; // 当needResult 为 1 时，扫码返回的结果
      alert(data);
      alert(res.resultStr);
      window.open(data);
      //处理自己的逻辑
    }
  });
};
```
这种写法写在wx.ready里就会报错the permission value is offline verifying,安卓下可以调用

### 基本解决方法 

the permission value is offline verifying这个错误是因为config没有正确执行，或者是调用的JSAPI没有传入config的jsApiList参数中。建议按如下顺序检查：

1.确认config正确通过。

2.如果是在页面加载好时就调用了JSAPI，则必须写在wx.ready的回调中。

3.确认config的jsApiList参数包含了这个JSAPI。

4.调用

```javascript
 let _data = data.data.jsapi;
  wx.config({
    debug: false,
    appId: _data.appId,
    timestamp: _data.timestamp,
    nonceStr: _data.nonceStr,
    signature: _data.signature,
    jsApiList: ['scanQRCode']
  });
  wx.scanQRCode({
    desc: 'scanQRCode desc',
    needResult: 1, // 默认为0，扫描结果由微信处理，1则直接返回扫描结果，
    scanType: ['barCode'], // 可以指定扫二维码还是一维码，默认二者都有
    success: function (res) {
      alert(res.resultStr);
    }
  });
```

### 最终解决方法

当以上这些都没有问题，created 里调的接口,分享的接口都通了，扫一扫的也是通的。我加了"checkJsApi"返回scanQRCode：true,但是还有有scanQRCode：the permission value is offline verifying的报错

地址栏问题:push的跳转不能被写入ios微信浏览器的地址栏

处理:push跳转改为window.loaction.href跳转 ;window.loaction.href跳转才能改变地址栏的变化，才能签名成功
